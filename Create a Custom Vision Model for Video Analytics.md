# What is Vision on Edge?

Vision on Edge (VoE) is an open-source solution template that accelerates the
process of building vision-based machine learning solutions that can be deployed
to edge devices. VoE helps you extract insights and actions from remote
networked cameras, using a no-code UI that processes streams on your
edge device. The Vision on Edge toolkit can be used to deploy pretrained machine
learning models to existing devices, or to create custom models tailored to
tasks in a specific environment.

Pretrained models, or AI Skills, support common tasks such as surveillance,
counting people or objects in an area, and detecting safety hazards. Custom
models can be trained to detect objects of your specification, to classify
people or things in a video stream, or to detect product logos on packaging or
in images.

In this quick start guide, you will learn how to set up the Azure environment
for managing a Vision on Edge solution, and then create a custom vision model as a resource that can be deployed to Azure or to a camera.

## How a Typical Solution Works

Assume that you have a camera set to record at intervals all day. After you
deploy your machine learning model to the camera, the API locally processes
images, checks the on-camera events, and identifies relevant objects or people.
If a relevant event occurs or an object is found, the AI notifies the system and
takes appropriate action. For example, the system might begin recording
continuously, turn on security lights, or save a thumbnail with a timestamp.

By putting the model on the camera, you can reduce false positive and greatly
reduce the time needed to review camera events. Popular uses for computer vision
include:

-   Monitoring room occupancy, compliance with health or safety measures

-   Tracking customer motion and behavior such as dwell times

-   Identifying objects or people in a video stream and generating an
    appropriate response

-   Counting people, or determining wait times in a queue

-   Extracting text from images and documents

# How to Create the Computer Vision Resource

## Prerequisites

-   An Azure account with Cognitive Services enabled.

-   A computer vision model, either custom or pretrained. Pretrained models are
    built for common scenarios using images provided by Microsoft. If a
    pretrained model does not meet your needs, you can create a custom model,
    based on tagged images that you provide.

-   A camera or camera emulator. If using your own camera, the camera should be
    an IP camera, network connected, with support for Real Time Streaming
    Protocol (RTSP), a network protocol designed for media such as a video
    stream from a CCTV or security camera system. Coaxial cameras cannot be used
    for projects that require RTSP unless paired with a compatible DVR.

-   To use the simulated camera provided by the Computer Vision service, see
    LINK.

-   Azure IoT Edge should be installed and running on your edge device.

## Set Up Azure Resources

1.  Log into the Azure Portal.

2.  Choose a resource group for deployment of the vision-related services.
    Because the cost of Cognitive Services varies by workload, you might want to
    create a separate resource group for these services. For guidance on
    pricing, see [Custom Vision pricing](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/custom-vision-service).

3.  If this is your first time using Cognitive Services, register your
    subscription as a Cognitive Services user. For demonstration purposes,
    choose the free (S0) service tier.

4.  After the service has been deployed, make a note of the endpoint and key
    from the resource management page.

## Create a Custom Vision Project

1.  To train a custom vision projects based on images that you provide, open
    the [Custom Vision AI](https://www.customvision.ai/) home page.

2.  Sign in using the account that you use in Azure.

3.  On the **Create New** **Resource** page, type a name for the custom vision
    test project.

4.  Select the Azure subscription and resource group where the solution will be
    deployed.

5.  Select a region, and leave the pricing tier as S0.

6.  By default, custom models use the option for both prediction and training, because the Custom Vision service is designed to support users who want to create machine learning models that are specific to a particular environment or image type. If you want to use one of the pretrained models from Microsoft or the community, select the **Computer Vision** service from the Cognitive Services menu.

7.  Click **Create Resources**, and when the dialog box refreshes, click
    **Create New**.

8.  At this point, you can select from among several scenarios in which vision
    plays an important role, and define the type of machine learning model you
    need:

    -   Classification supports identification of objects or people.

    -   Object detection models are specific to a type of image or object.

    -   When choosing a model, consider whether each of the training images you
    provide contains a single object, or multiple objects. For example, if you
    want to identify both cats and dogs, and some images contain both cats and
    dogs, you would choose the Multilabel option, which allows multiple tags per
    image.

    -   Each of the model types supported by Computer Vision works best in specific
    domains:

        -   Classification / Multilabel: General, food, Landmarks, Retail

        -   Classification / Multiclass: General, food, Landmarks, Retail

        -   Object Detection: General, Logo, Objects on shelves

    -   **Important: Deployment to an edge device requires that the model be created using one of the Compact formats.**

1.  After selecting the appropriate model, click **Create**.

2.  Upload images you have collected for use in training the model. For example, if you want to identify logos, you would upload multiple different images containing the logos you want to identify. Typically at least 15 images are required for each item you want to identify or classify.

3.  After the images are loaded into your workspace, you can tag them with the name of the target object. You can tag individual images by clicking on the target area, and typing a label name, or tag. If your image contains
 multiple objects, you can highlight each region separately and assign tags,though it is best if regions do not overlap. Tagging goes faster if you upload related images in one batch, and then type a single tag to apply to all images.

4.  Use the sliders to set the threshold for determining precision and recall, which defaults to 50%. Likewise, set the **Overlap Threshold**, which defines the amount of overlap between regions allowed for a correct prediction.

5.  When you have tagged all the images, click **Train**, and choose **Quick Train**, or **Advanced Train**. The Advanced Train option is recommended for challenging and fine-gained datasets. 

6.  If you do not have enough images for each label or tag, an error is raised, but you can easily go back and add images.

7.  After training is complete, scores are automatically computed for precision, recall, and mean average precision. You can also test the model by providing a local image, or image as URL, to determine whether the prediction is correct.

8.  Open the **Projects** page, and view the size of the model, when it was trained, and the resource ID. If you are satisfied with the performance of the model, click **Publish** to create an endpoint and key for the model resource.

## Call Your Model from an App

1.  Return to the Azure portal, and the new Cognitive Services resource for the custom vision test model should be available in the specified resource group.

2.  There are two ways to use the completed model: you can deploy it to an edge device, such as an RSTP camera, or you can create an app to call the model and get and send requests to the camera. See the **Next Steps** for detailed information and walkthroughs on these scenarios.

# Next steps

Overview of video analytics capabilities in Azure

-   <https://azure.microsoft.com/en-us/blog/azure-introduces-new-capabilities-for-live-video-analytics/>

Tips for making your cameras work better for specific tasks and environments

-   [Spatial Analysis camera placement - Azure Cognitive Services \| Microsoft
    Docs](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/spatial-analysis-camera-placement)

Use Azure functions to call AI skills

-   [Azure
    Functions](https://docs.microsoft.com/en-us/azure/search/cognitive-search-create-custom-skill-example)

Developer walkthrough: calling Custom Vision resource from C\# or Python

-   [Analyze live video with Video Analyzer on IoT Edge and Azure Custom Vision
    \| Microsoft
    Docs](https://docs.microsoft.com/en-us/azure/azure-video-analyzer/video-analyzer-docs/edge/analyze-live-video-custom-vision?pivots=programming-language-csharp)
