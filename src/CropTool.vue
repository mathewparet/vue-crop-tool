<template>
    <span>
        <input type="file" name="avatar" accept="image/*" @change="fileChanged(this)" ref="file">
        <slot></slot>
        <slot name="canvas" v-if="this.canvas!='undefined'"><img src="" width="100" ref="canvas" /></slot>
    </span>
</template>

<script>
    import Cropper from 'cropperjs';
    let CropTool = {
        install(Vue)
        {
            Vue.component('crop-tool', CropTool);
        },
        props: [
            'preview',
            'canvas',
            'value',
        ],
        data() {
            return {
                file: null,
                url: null,
                image: null,
                options: {},
                cropper: null,
            }
        },
        mounted() {
            this.url = window.URL || window.webkitURL;
            this.cropper = window.Cropper;
            this.file = this.$refs.file;
            this.options.aspectRatio = 1 / 1;
            this.options.preview = '.'+this.preview;
            this.image = this.canvas ? document.getElementById(this.canvas) : this.$refs.canvas;
        },
        methods: {
            fileChanged($el) {
                var files = this.file.files;
                var file;

                if (files && files.length) 
                {
                    file = files[0];

                    if (/^image\/\w+/.test(file.type)) 
                    {
                        this.url = window.URL || window.webkitURL;
                        this.image.src = this.url.createObjectURL(file);
                        try
                        {
                            this.cropper.destroy();
                        }
                        catch(Exception)
                        {
                            ;
                        }
                        this.cropper = new Cropper(this.image, this.options);

                        this.image.addEventListener('cropend',this.imageReady);
                        this.image.addEventListener('ready',this.imageReady);
                        this.image.addEventListener('zoom',this.imageReady);

                        this.file.value = null;
                    }
                    else 
                    {
                        window.alert('Please choose an image file.');
                    }
                }
            }
            , imageReady() {
                this.$emit('input',this.cropper.getCroppedCanvas().toDataURL('image/png'))
            }
        }
    }
    export default CropTool;
</script>
