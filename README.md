"# ionic-camera-gallery" 

```Typescript
import { Component, EventEmitter, OnInit, Output, ViewChild } from '@angular/core';
import { Camera, CameraOptions } from '@ionic-native/camera/ngx';
import { File } from '@ionic-native/file/ngx';
import { WebView } from '@ionic-native/ionic-webview/ngx';
import { DomSanitizer } from '@angular/platform-browser';

@Component({
    selector: 'app-photo',
    templateUrl: './photo.page.html',
    styleUrls: ['./photo.page.scss'],
})
export class PhotoPage implements OnInit {

    cameraOptions: CameraOptions = {
        quality: 100,
        destinationType: this.camera.DestinationType.FILE_URI,
        encodingType: this.camera.EncodingType.JPEG,
        mediaType: this.camera.MediaType.PICTURE
    }

    galleryOptions: CameraOptions = {
        quality: 60,
        destinationType: this.camera.DestinationType.FILE_URI,
        encodingType: this.camera.EncodingType.JPEG,
        mediaType: this.camera.MediaType.PICTURE,
        correctOrientation: true,
        sourceType: this.camera.PictureSourceType.PHOTOLIBRARY
    };


    constructor(
        private camera: Camera,
        private webview: WebView,
    ) { }

    async ngOnInit() {
    }

    camara() {
        let options: CameraOptions = {
            quality: 100,
            destinationType: this.camera.DestinationType.FILE_URI,
            encodingType: this.camera.EncodingType.JPEG,
            mediaType: this.camera.MediaType.PICTURE,
            correctOrientation: true,
            sourceType: this.camera.PictureSourceType.CAMERA
        }

        this.procesarImagen(options);
    }

    galeria() {
        let options: CameraOptions = {
            quality: 60,
            destinationType: this.camera.DestinationType.FILE_URI,
            encodingType: this.camera.EncodingType.JPEG,
            mediaType: this.camera.MediaType.PICTURE,
            correctOrientation: true,
            sourceType: this.camera.PictureSourceType.PHOTOLIBRARY
        };

        this.procesarImagen(options);
    }


    async procesarImagen(options: CameraOptions) {
        this.camera.getPicture(options).then((img) => {
            const tempFilename = img.substr(img.lastIndexOf('/') + 1);
            const src = this.webview.convertFileSrc(img);

            console.log(tempFilename); // image name
            console.log(src); //image url from movil

        });
    }

}
```

"# Obtain image from mobile" 

```Typescript
 exportarImagenes(imagenes[]) {
    let formData = new FormData();
    let response: any;
    let blob: any;

    imagenes.forEach(async (element) => {
      const url = element.url.split('?')[0];
      response = await fetch(url);
      blob = await response.blob();  // imagen in blob format
      formData = new FormData();
      formData.append("file", blob, element.nombre.split('?')[0]);
    });
  }
```
