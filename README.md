# @mathewparet/vue-crop-tool

> A tool to easily crop input image. Works like a normal input.

## Build Setup

``` bash
# install dependencies
npm install

# build for production with minification
npm run build
```

## Global Import
``` js
import CropperBox from '@mathewparet/vue-crop-tool';
Vue.use(CropperBox);
```

## Usage Example

``` html
<div class="form-group row">
    <label for="avatar" class="col-md-4 col-form-label text-md-right">Avatar</label>
    <div class="col-md-6">
        <crop-tool name="avatar" preview="avatar-preview" canvas="avatar-crop-space" v-model="form.avatar">
            <span class="form-text text-muted">
                Required only if you wish to change current profile picture.
            </span>
        </crop-tool>
        <img src="" id="avatar-crop-space" width="100" />
    </div>
</div>
<div>
    <div class="avatar-preview rounded-circle" id="profile-pic" style="overflow: hidden; width: 140px; height: 140px; background: url('//via.placeholder.com/140x140/ffffff/?text=Preview')"></div>
</div>
```

## Attributes

| Name | Description | Required? |
|---|---|---|
| preview | The class name of the ```<div>``` element within which the preview will be shown. | Yes |
| canvas | The DOM ID of the ```<img>``` element that use used as the crop space | Yes |

## Notes

1. To limit the crop size, set the width and height of the preview ```<div>```.
1. The cropped value will be returned in the ```v-model```.
1. ```v-model``` can't be used to set the initial value.