<h1>Understanding how the image is built. zeroConditioning, clipVision, seed and prompt injection </h1>
Are we sure we understand how the image is built and what reference the prompt image is based on?

Since [@cubiq](https://github.com/cubiq/prompt_injection) creation of the prompt injection node, I have discovered that what I thought about image creation in comfyUI is probably not what I imagined.  

Before I begin my demonstration. I invite you to read the first part of Prompt Injection (https://github.com/Creative-comfyUI/prompt_injection) . You can also read what I have written about seeds (https://github.com/Creative-comfyUI/seed_eng). All this information is necessary to understand what I am about to demonstrate. 

In my previous repisotery about prompt injection, <b>I explained that even prompt is muted with zeroConditioning, ksampler generated image </b>. <b>This image looks like a reference</b>. You have to understand that no text in the clip text encoding doesn't mean that the prompt is muted. The zeroConditioning ensures that no text information is used by the clip (https://openai.com/index/clip/). 

The image generated by zeroConditioning is a reference image. There is something tricky about. Using batch size 3 show us that there is more than one reference image. One is a reference at the beginning of the process and the other one is a reference for the end of the process. You think I am crazy? Not at all. Let us see with examples.

Before, it is important to understand for some reasons that <b>Sdxl Turbo, Lightning and in general few steps model give the best result and more accurate in all the process</b>. For all my examples I will use the sdxl model. SD 1.5 may be different. <b>I will use Euler as I explain before Euler always give the same image for a batch size</b>. I'm also using Ksampler Advanced (inspire) to make sure that comfyUI doesn't add noise variation.

First I will generate an image with a few steps model with a radom seed. Size 832 * 1216 . Batch size 1 

Here is the result  
![Screenshot 2024-06-13 at 1 55 00 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/bf267d74-a5a0-4fa4-be49-8c068cec0738)

We will keep the same seed and fix it and generate a batch size of 3 this time. 

Here is the result 

![Screenshot 2024-06-13 at 2 04 18 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/1e0cc15b-5a81-401e-b871-f4d638db8a4f)

Everything is fine as we have the same images as we use Euler

Now we are going to use prompt injection to see what has happened.

We will link an empty clip Text Encode to output 8.  

Here is the result 

![Screenshot 2024-06-13 at 3 19 55 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/dea90ee1-5324-4d49-99ef-d10785cd06a7)

<b>The third image is different from the others. This is what I called the second reference</b>. 

Now we are going to write a text in the clip prompt injection of output 8.

![Screenshot 2024-06-13 at 3 27 31 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/b43eb923-ab8f-481f-bc66-968d4cb424ea)

Now we are going to take the same prompt and use it as usual and unlink the prompt injection. 

Here is the result 

![Screenshot 2024-06-13 at 4 58 33 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/f432e798-6cb0-4ee0-8778-af96ead9d36f)

As you can see, all the colour and tone is linked to the first reference images of the landscape we see before. As you can see, this time the building has disappeared. What does this mean? The first image reference can be considered as the general ambiance (colour, luminosity ....) and the third image would affect the theme depending on what you wrote in a prompt, this case is less striking than the image in part one. We can assume that it is a mixture of noise reference 1 and noise reference 2 You are not convinced? Let us try the reverse process with Clip Vision 

Clip Vision help to use an image instead of a prompt to render a batch of images 

We are going to use the last image with the same seed 

![workflow-8](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/7ecb84ee-19ee-4a99-9bfc-1067ac7cb7d6)

We first use 1 for the strength of the unClipConditioning and then 0. 1 is refering to second image et 0 to first image 

![Screenshot 2024-06-13 at 6 33 58 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/dd968c4d-52d5-4bc4-b86c-27610bfb4d76) ![Screenshot 2024-06-13 at 6 33 52 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/dbc99b73-e0e1-4741-8de3-acfa6721f5bc)

As you can see, we see the same perspective and building from both parts.

For 0 we have the same image as before 

![Screenshot 2024-06-13 at 6 36 33 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/1a388b69-14dc-427a-808f-fe4ce254b7a8)

Your are still not convince ? Here is another, image used in part 1. If the image doesn't look sharp, it's because I didn't use the sampler suggested for this model. This point is very important and made a big difference to the result. 

![ImageComparaison](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/93646d4b-6373-4492-8a2f-08597d8a9925)

The original base image 

![Screenshot 2024-06-13 at 7 17 51 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/1a74b716-3662-428f-856e-7f78cf13eff0)  ![Screenshot 2024-06-13 at 7 17 59 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/9f68aef3-0e9d-473e-8cb7-3f113bbb0d2b)

What does this mean? It means that depending on what you want to build, it may be good to randomise images using Zeroconditioning and PromptInjection to decide which image to start with. This is why the seed is important, it determines which image we will use and use it as a reference. 

But it is not always as easy as we thought. Let us try to make changes and see what happens. 

With the same seed let us try different sampler using clipvision 

![Screenshot 2024-06-13 at 11 08 17 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/57aa99ac-357c-4869-9e48-6c46cd4dd3d6)  ![Screenshot 2024-06-13 at 11 04 58 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/45f7d2b0-1880-4dc0-9bb0-49ac673ac303)

Different samplers don't change the image. it plays on detail. The seeds preserve the image

Now randomise the seeds and see what happens for strength 0, 0.5 1 for the same seed 

![Screenshot 2024-06-13 at 11 49 50 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/f6f3caed-f162-42dd-a630-b79c8d051215) ![Screenshot 2024-06-13 at 11 47 18 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/d163eadc-7e69-4b9d-868b-7d0728459656) ![Screenshot 2024-06-13 at 11 42 54 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/e3c96c43-32b1-4347-b281-8dd9aa35d322)

Theses images can let us figure out what can be the base image. Let us retrieve the base image 

This time we will go back to our original work, use the new seed with zeroconditioning and prompt injection output 8 and see what happens. 

![Screenshot 2024-06-13 at 11 53 27 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/b98a7fa7-ec4e-4e17-affb-8d7e18353e64) 

As you can see we retrieve the image that we have with clipvision. This time the 2 images reference is quiet the same. 

Now we know that the image we create is the result of two random images. The question is why two images, and how is it that the second has more influence than the first? 

Prompt injection can be a key changer, giving us better control over the final image and designing what is more important or dominant. 





