  - [Getting started](#getting-started)
  - [Android](#android)
  	- [Sample applications](#sample-applications-android)
		- [Benchmark](#sample-application-benchmark-android)
		- [VideoParallel](#sample-application-videoparallel-android)
		- [videoSequential](#sample-application-videosequential-android)
		- [ImageSnap](#sample-application-imagesnap-android)
	- [Trying the samples](#trying-the-samples-android)
	- [Adding the SDK to your project](#adding-the-sdk-to-your-project-android)
	- [Using the Java API](#using-the-java-api-android)
 - [Raspberry Pi (Raspbian OS) and others](#others)
 	- [Sample applications](#sample-applications-others)
		- [Benchmark](#sample-application-benchmark-others)
		- [Recognizer](#sample-application-recognizer-others)
 - [Getting help](#technical-questions)
  
 - Full documentation at https://www.doubango.org/SDKs/anpr/docs/
 - Online demo at https://www.doubango.org/webapps/alpr/
  
<hr />
  
Have you ever seen a deep learning based [ANPR/ALPR (Automatic Number/License Plate Recognition)](https://en.wikipedia.org/wiki/Automatic_number-plate_recognition) engine running at **47fps on ARM device** (Android, Snapdragon 855, 720p video resolution)? <br />

With an average frame rate as high as **47 fps on ARM** devices (Snapdragon 855) this is the fastest ANPR/ALPR implementation you'll find on the market. 
Being fast is important but being accurate is crucial. 
We use state of the art deep learning techniques to offer unmatched accuracy and precision. As a comparison this is **#33 times faster than** [OpenALPR on Android](https://github.com/SandroMachado/openalpr-android).
(see [benchmark section](https://www.doubango.org/SDKs/anpr/docs/Benchmark.html) for more information).

No need for special or dedicated GPUs, everything is running on CPU with **SIMD ARM NEON** optimizations, fixed-point math operations and multithreading.
This opens the doors for the possibilities of running fully featured [ITS (Intelligent Transportation System)](https://en.wikipedia.org/wiki/Intelligent_transportation_system) solutions on a camera without soliciting a cloud. 
Being able to run all ITS applications on the device **will significantly lower the cost to acquire, deploy and maintain** such systems. 
Please check [Device-based versus Cloud-based solution](https://www.doubango.org/SDKs/anpr/docs/Device-based_versus_Cloud-based_solution.html) section for more information about how this would reduce the cost.

<p align="center" style="text-align: center">
  <img src="https://www.doubango.org/SDKs/anpr/docs/_images/theverge_with_pysearch.jpg">
  <br />
  <em><u><a href="#sample-application-videoparallel-android">VideoParallel sample application</a> on Android</u></em>
</p>

We're already working to bring this frame rate at 64fps and add support for CMMDP (**Color-Make Model-Direction-Prediction**) before march 2020. 
We're confident that it's possible to have a complete [ITS](https://en.wikipedia.org/wiki/Intelligent_transportation_system) (**license plate recognition, CMMDP, bus lane enforcement, red light enforcement, speed detection, 
congestion detection, double white line crossing detection, incident detection...**) system running above 40fps on ARM device.

On high-end NVIDIA GPUs like the **Tesla V100 the frame rate is 315 fps which means 3.17 millisecond inference time**.
On low-end CPUs like the **Raspberry Pi 4 the average [frame rate is 12fps](samples/c++/benchmark/README.md#peformance-numbers)**.

Don't take our word for it, come check our implementation. **No registration, license key or internet connection is required**, just clone the code and start coding/testing. Everything runs on the device, no data is leaving your computer. 
The code released here comes with many ready-to-use samples for [Android](#sample-applications-android) and [Raspberry Pi](#sample-applications-others) to help you get started easily. 

You can also check our online [cloud-based implementation](https://www.doubango.org/webapps/alpr/) (*no registration required*) to check out the accuracy and precision before starting to play with the SDK.

Please check full documentation at https://www.doubango.org/SDKs/anpr/docs/

<a name="getting-started"></a>
# Getting started # 
The SDK works on [many platforms](https://www.doubango.org/SDKs/anpr/docs/Architecture_overview.html#supportedoperatingsystems) and comes with support for many [programming languages](https://www.doubango.org/SDKs/anpr/docs/Architecture_overview.html#supportedprogramminglanguages) but the next sections focus on [Android](#android) and [Raspberry pi](#others). 

<a name="android"></a>
# Android #

The next sections are about Android and Java API.

<a name="sample-applications-android"></a>
## Sample applications (Android) ##
The source code comes with #4 Android sample applications: [Benchmark](#sample-application-benchmark-android), [VideoParallel](#sample-application-videoparallel-android), [VideoSequential](sample-application-videosequential-android) and [ImageSnap](sample-application-imagesnap-android).

<a name="sample-application-benchmark-android"></a>
### Benchmark (Android) ###
This application is used to check everything is ok and running as fast as expected. The information about the maximum frame rate (**47fps**) on Snapdragon 855 devices could be checked using this application. It's open source and doesn't require registration or license key.

<a name="sample-application-videoparallel-android"></a>
### VideoParallel (Android) ###
This application should be used as reference code by any developer trying to add ultimateALPR to their products. It shows how to detect and recognize license plates in realtime using live video stream from the camera.
Please check [Parallel versus sequential processing section](https://www.doubango.org/SDKs/anpr/docs/Parallel_versus_sequential_processing.html#parallelversussequentialprocessing) for more info about parellel mode.

<a name="sample-application-videosequential-android"></a>
### VideoSequential (Android) ###
Same as VideoParallel but working on sequential mode which means slower. This application is provided to ease comparing the modes: Parallel versus Sequential.

<a name="sample-application-imagesnap"></a>
### ImageSnap (Android) ###
This application reads and display the live video stream from the camera but only recognize an image from the stream on demand.

<a name="trying-the-samples-android"></a>
## Trying the samples (Android) ##
To try the sample applications on Android:
 1. Open Android Studio and select "Open an existing Android Studio project"
![alt text](https://www.doubango.org/SDKs/anpr/docs/_images/android_studio_open_existing_project.jpg "Open an existing Android Studio project")

 2. Navigate to **ultimateALPR-SDK/samples**, select **android** folder and click **OK**
![alt text](https://www.doubango.org/SDKs/anpr/docs/_images/android_studio_select_samples_android.jpg "Select project")

 3. Select the sample you want to try (e.g. **videoparallel**) and press **run**. Make sure to have the device on **landscape mode** for better experience.
![alt text](https://www.doubango.org/SDKs/anpr/docs/_images/android_studio_select_samples_videoparallel.jpg "Select sample")
            
<a name="adding-the-sdk-to-your-project-android"></a>
## Adding the SDK to your project (Android) ##
The SDK is distributed as an Android Studio module and you can add it as reference or you can also build it and add the AAR to your project. But, the easiest way to add the SDK to your project is by directly including the source.

In your *build.gradle* file add:

```python
android {

      # This is the block to add within "android { } " section
      sourceSets {
         main {
             jniLibs.srcDirs += ['path-to-your-ultimateALPR-SDK/binaries/android/jniLibs']
             java.srcDirs += ['path-to-your-ultimateALPR-SDK/java/android']
             assets.srcDirs += ['path-to-your-ultimateALPR-SDK/assets/models']
         }
      }
}
```

<a name="using-the-java-api-android"></a>
## Using the Java API (Android) ##

It's hard to be lost when you try to use the API as there are only 3 useful functions: init, process and deInit.

The C++ API is defined [here](https://www.doubango.org/SDKs/anpr/docs/cpp-api.html).

```java

	import org.doubango.ultimateAlpr.Sdk.ULTALPR_SDK_IMAGE_TYPE;
	import org.doubango.ultimateAlpr.Sdk.UltAlprSdkEngine;
	import org.doubango.ultimateAlpr.Sdk.UltAlprSdkParallelDeliveryCallback;
	import org.doubango.ultimateAlpr.Sdk.UltAlprSdkResult;

	final static String CONFIG = "{" +
		"\"debug_level\": \"info\"," + 
		"\"gpgpu_enabled\": true," + 

		"\"detect_minscore\": 0.1," + 
		"\"detect_quantization_enabled\": true," + 
		
		"\"pyramidal_search_enabled\": true," +
		"\"pyramidal_search_sensitivity\": 0.28," +
		"\"pyramidal_search_minscore\": 0.5," +
		"\"pyramidal_search_quantization_enabled\": true," +

		"\"recogn_score_type\": \"min\"," + 
		"\"recogn_minscore\": 0.3," + 
		"\"recogn_rectify_enabled\": false," + 
		"\"recogn_quantization_enabled\": true" + 
	"}";

	/**
	* Parallel callback delivery function used to notify about new results.
	* This callback will be called few milliseconds (before next frame is completely processed)
	* after process function is called.
	*/
	static class MyUltAlprSdkParallelDeliveryCallback extends UltAlprSdkParallelDeliveryCallback {
		@Override
		public void onNewResult(UltAlprSdkResult result) { }
	}

	final MyUltAlprSdkParallelDeliveryCallback mCallback = new MyUltAlprSdkParallelDeliveryCallback(); // set to null to disable parallel mode

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		

		// Initialize the engine
		assert UltAlprSdkEngine.init(
				getAssets(),
				CONFIG,
				mCallback
		).isOK();
	}

	// Camera listener: https://developer.android.com/reference/android/media/ImageReader.OnImageAvailableListener
	final ImageReader.OnImageAvailableListener mOnImageAvailableListener = new ImageReader.OnImageAvailableListener() {

		@Override
		public void onImageAvailable(ImageReader reader) {
				try {
				    final Image image = reader.acquireLatestImage();
				    if (image == null) {
				        return;
				    }

				    // ANPR/ALPR recognition
				    final Image.Plane[] planes = image.getPlanes();
				    final UltAlprSdkResult result = UltAlprSdkEngine.process(
				        ULTALPR_SDK_IMAGE_TYPE.ULTALPR_SDK_IMAGE_TYPE_YUV420P,
				        planes[0].getBuffer(),
				        planes[1].getBuffer(),
				        planes[2].getBuffer(),
				        image.getWidth(),
				        image.getHeight(),
				        planes[0].getRowStride(),
				        planes[1].getRowStride(),
				        planes[2].getRowStride(),
				        planes[1].getPixelStride()
				    );
				    assert result.isOK();

				    image.close();

				} catch (final Exception e) {
				   e.printStackTrace();
				}
		}
	};

	@Override
	public void onDestroy() {
		// DeInitialize the engine
		assert UltAlprSdkEngine.deInit().isOK();

		super.onDestroy();
	}
```

Again, please check the sample applications for [Android](#sample-applications-android) and [Raspberry Pi](#sample-applications-others) and [full documentation](https://www.doubango.org/SDKs/anpr/docs/) for more information.

<a name="others"></a>
# Raspberry Pi (Raspbian OS) and others #

<a name="sample-applications-others"></a>
## Sample applications (Raspberry Pi) ##
The source code comes with #2 [C++ sample applications](samples/c++): [Benchmark](#sample-application-benchmark-others) and [Recognizer](#sample-application-recognizer-others). These sample applications can be used on all supported platforms: **Android**, **Windows**, **Raspberry pi**, **iOS**, **OSX**, **Linux**...

<a name="sample-application-benchmark-others"></a>
### Benchmark (Raspberry Pi) ###
This application is used to check everything is ok and running as fast as expected. 
The information about the maximum frame rate (**47fps** on Snapdragon 855 devices and **12fps** on Raspberry Pi 4) could be checked using this application. 
It's open source and doesn't require registration or license key.

For more information on how to build and run this sample please check [samples/c++/benchmark](samples/c++/benchmark/README.md).

<a name="sample-application-recognizer-others"></a>
### Recognizer (Raspberry Pi) ###
This is a command line application used to detect and recognize a license plate from any JPEG/PNG/BMP image.

For more information on how to build and run this sample please check [samples/c++/recognizer](samples/c++/recognizer/README.md).

<a name="technical-questions"></a>
 # Technical questions #
 Please check our [discussion group](https://groups.google.com/forum/#!forum/doubango-ai) or [twitter account](https://twitter.com/doubangotelecom?lang=en)
