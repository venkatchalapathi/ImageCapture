# ImageCapture

Request the camera feature
If an essential function of your application is taking pictures, then restrict its visibility on Google Play to devices that have a camera. To advertise that your application depends on having a camera, put a <uses-feature> tag in your manifest file:

    <manifest ... >
        <uses-feature android:name="android.hardware.camera"
                  android:required="true" />
         ...
    </manifest>
    
    
## Take a photo with a camera app

The Android way of delegating actions to other applications is to invoke an Intent that describes what you want done. This process involves three pieces: The Intent itself, a call to start the external Activity, and some code to handle the image data when focus returns to your activity.

Here's a function that invokes an intent to capture a photo.

    static final int REQUEST_IMAGE_CAPTURE = 1;

    private void dispatchTakePictureIntent() {
      Intent takePictureIntent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
       if (takePictureIntent.resolveActivity(getPackageManager()) != null) {
        startActivityForResult(takePictureIntent, REQUEST_IMAGE_CAPTURE);
      }
     }
  
  ## Get the thumbnail
  
  The Android Camera application encodes the photo in the return Intent delivered to onActivityResult() as a small Bitmap in the extras, 
  under the key "data". The following code retrieves this image and displays it in an ImageView.
  
        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        if (requestCode == REQUEST_IMAGE_CAPTURE && resultCode == RESULT_OK) {
         Bundle extras = data.getExtras();
         Bitmap imageBitmap = (Bitmap) extras.get("data");
         imageView.setImageBitmap(imageBitmap);
         }
        }
        
        
 Source Linkss
   https://developer.android.com/training/camera/photobasics
