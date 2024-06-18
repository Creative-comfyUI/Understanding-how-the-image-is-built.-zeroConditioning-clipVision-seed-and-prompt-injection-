<h1>Understanding how the image is built. zeroConditioning, clipVision, seed and prompt injection </h1>
Are we sure we understand how the image is built and what reference the prompt image is based on?

Since [@cubiq](https://github.com/cubiq/prompt_injection) creation of the prompt injection node, I have discovered that what I thought about image creation in comfyUI is probably not what I imagined.  

Before I begin my demonstration. I invite you to read the first part of Prompt Injection (https://github.com/Creative-comfyUI/prompt_injection) . You can also read what I have written about seeds (https://github.com/Creative-comfyUI/seed_eng). All this information is necessary to understand what I am about to demonstrate. 

In my previous repisotery about prompt injection, <b>I explained that even prompt is muted with zeroConditioning, ksampler generated image </b>. <b>This image looks like a reference</b>. You have to understand that no text in the clip text encoding doesn't mean that the prompt is muted. The zeroConditioning ensures that no text information is used by the clip (https://openai.com/index/clip/). 

The image generated by zeroConditioning appears to be a reference image, but how it is used is the question. It is probably the noise that is used.  What we are sure of is that for each seed the model produces an image, even without a prompt. For the same seed, there is a similarity between the images rendered (example: a man, a room, a garden.... ). What surprised me was that each model didn't give the same finishing touch to the image reference, some are blured, some are not well defined and others are a perfect photo. Let us look at a few examples with the same seeds and zero conditioning. 

![Model_Euler](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/c7580084-e179-4160-96f2-d81d6b5ef9f2)

The most intriguing is that the sampler can give a different image. Many users thought that the sampler influenced the finishing of the image. Sampler can influence much more the images. Lets have a look at some example with always zeroConditioning and same seed. 

![Sampler](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/62accb8d-e2e4-49f3-b6c2-31066a05e182)

There is another surprise the format can change the reference image too 

![Size](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/dbfa819e-6cff-4ea2-9521-9554b758c4ca)

Now let us use prompt injection to see what has happened. As I mentioned in my previous repository, output 8 is the key change of the image. Not for the first image, but for the third more than the second. Output 8 with an empty prompt affected the result. The most defined reference image will show the more important change. Example with Sdxl 1 the change is slight.  Let us look at some examples. 

This example is with sdxl_ligthning_8step model 

![Screenshot 2024-06-16 at 2 38 21 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/675859cc-039f-4901-837b-434a8feddae0)

If we change the size to 832 * 1216 the third image is completely different, which is not the case when using Euler. This output 8 change the image 

![Screenshot 2024-06-16 at 2 45 07 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/73b2d6c1-eead-42df-9c25-975a18ba0b9a)

Before continuing, write a prompt and mute the negative prompt to see what the result is for each model without prompt injection. 

Prompt : Paris champ de mars, an elegant woman colorfull, in 1950 style

![Model_Prompt](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/6f8d9009-6671-4b81-8c8d-1497a41930fb)

Now let try If as previously sampler change the image. I am going the same model and the same sampler and see the results 

![Sampler_Prompt](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/b57a2672-eef1-4469-8ef7-aceb2f0efc30)

The results obtained with different samplers show us that the image is in relation to the reference image style (realistic, drawin, sketching...) but it is not always the case 

All these images are in 1024 * 1024 format, which means that with another the result will be different. 

w 832 * h 1216 

![Screenshot 2024-06-16 at 7 18 29 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/09ce416b-0b76-4a12-a8a1-c9a1333e8322)

w 1536 * 640 

![Screenshot 2024-06-16 at 7 43 30 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/3ba7bfa5-c599-47af-9eb7-57e5714d0485)

Times to times with bigger images we can see a signature on the image or text as with this image without being able to read it. 

What is commun with all these images ? 

The Eiffel Tower, because it is associated with the Champ de Mars in Paris, cars, an elegant lady in a hat and, finally, nice colours. 

Before continuing the explanation, we can conclude that Euler samplers always give the same images. Other samplers may give different images or style. The image following the first image can be different from the others with samplers other than Euler. The first picture is a kind of reference. The seed is linked to this image. Changing the size of the image changes the point of view and can change the image. It looks like the image is related to the deep field of the camera. 1526 * 640 can be considered as f22. 

Now we are going to use prompt injection as it can change many things in the result of the image. 

Adding an empty prompt to output 8 add variation to image 2 and 3. 3 has much more variation. Image 1 didn't change 

![Screenshot 2024-06-16 at 8 30 33 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/898e50ab-2f50-4c7b-8a49-c40a75c0e8fa)

Now I will go to the muted prompt and write the prompt in the one that links to output 8 

![Screenshot 2024-06-16 at 10 58 17 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/13363592-3f64-4a93-897d-0efebea52597)

This means that the apply prompt in input 8 doesn't create an image, but gives a variation of the image reference, because images 2 and 3 are different. Input 8 will create a variation no matter what you write. This means that if you have a good reference image you can use it to make a variation using input 8  and using batch size 3, depending on the model and latent size the variation may be less important and less or more interesting. Output 0 and 1 will help to add detail to these variations. Let us take a look at the previous examples using the DreamshaperXL mode and the LCM sampler. I use zeron conditionning for the prompt and the input 8 prompt is blank here is the result 

![LCM input_8](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/488c4ac4-0809-4ffb-833e-228aa1e470bc)

Now are going to add details to image 2 and 3 using different input and ouput 

input 5 and input 8 with blank prompt change face expression of the third image 

![visage](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/ed8edfa3-2ea5-4117-8bb9-5c057a9a1d36)

input 7  and input 8 with blank prompt change much more face expression of the third image 

![visage2](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/ef3d2c02-52a1-4c18-bd99-1f14b8f6f460)

Now we are going to use prompt with input 0 and input 1 

input 0 : woman smiling and dancing with hands up
input 1 : Red jacket, blue trouser, yellow hat, 

![Screenshot 2024-06-17 at 8 23 33 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/7e7167c1-7a46-4484-a0d0-58231cb79ee0)

Now I will link all to a prompt in prompt injection. The prompt is the one in front of Paris champ de mars, an elegant woman colourful, in 1950 style
This prompt changes the second image, but the prompt was not applied. If we disconnect input 8 and keep all outputs 1 and 0, then not only the third image but also the second one will be affected. 
This time the output prompt 0 and 1 are correctly applied, but it is not the prompt we expected.

![Screenshot 2024-06-17 at 8 42 13 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/4e6cf9d0-8249-47fe-a7a5-574f26500d34) ![Screenshot 2024-06-17 at 10 09 27 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/5a9a373a-c3c3-40e4-8319-c0d8b7612ea6)

If we now change the Lcm sampler for dpmpp_2m with input 8, the result is different. The second image is the metamorphosis of the reference image and the third image is the final transformation. 

![Screenshot 2024-06-17 at 9 25 10 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/fd6106ab-def8-4c7a-9c4c-4ecc424b042c)

Now we applied the current prompt and prompt injection all, output 0 and output 1 applied, without injection all and without injection all and dpmmp_sde sampler instead Lcm 

![Screenshot 2024-06-17 at 10 23 57 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/22203c2c-91f5-4173-9ad5-e011486c2ad9) ![Screenshot 2024-06-17 at 9 57 39 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/573ab13b-4124-4e08-90b1-9d10963dad0e) ![Screenshot 2024-06-17 at 10 42 38 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/9b9b2a50-f151-4754-bd94-7d01b1fefd7f)




The question is: is there a relationship between the reference image and the final image, or is it a glitch ? Is the reference image an AI image or an existing image that was used to train the AI? 
Prompt injection bring precision and detail to the image.

Let tryied to use this image as a latent with 









The image generated by zeroConditioning is a reference image. There is something tricky about. Using batch size 3 show us that there is more than one reference image. One is a reference at the beginning of the process and the other one is a reference for the end of the process. You think I am crazy? Not at all. Let us see with examples.

Before, it is important to understand for some reasons that <b>Sdxl Turbo, Lightning and in general few steps model give the best result and more accurate in all the process</b>. For all my examples I will use the sdxl. SD 1.5 may be different. <b>I will use Euler as I explain before Euler always give the same image for a batch size</b>. I'm also using Ksampler Advanced (inspire) to make sure that comfyUI doesn't add noise variation.

First I will generate an image with a few steps model with a radom seed. Size 832 * 1216 . Batch size 1. Few steps models seems to be different thant other models 

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

![Screenshot 2024-06-13 at 11 53 27 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/b98a7fa7-ec4e-4e17-affb-8d7e18353e64) ![Screenshot 2024-06-14 at 12 01 36 AM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/284abd3b-6a64-4323-8e7a-de6868bc4144)

As you can see we retrieve the image that we have with clipvision. This time the 2 images reference is quiet the same.

Now we know that the image we create is the result of two random images. The question is why two images, and how is it that the second has more influence than the first? 

Before we go any further, using a regular SDXL (Stability AI model)  is quite different. Keeping the same seed, we will change the model and see what happens.

This time there are no image references. There is a single undefined image

![Screenshot 2024-06-14 at 12 25 36 AM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/0321500e-48d2-4007-8ee7-11b8766d7338)

Does this mean that the model like the Turbo or the ones with few steps to shorten the processus use images instead of undefined image? 

Let try the SDXL Turbo of Stability AI. This time we have an image, a single image 

![Screenshot 2024-06-14 at 1 08 20 AM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/bb702cb6-4844-486d-ad7c-143c912856ba)

Does this mean that the models we have don't follow the rules defined by Stability AI?   Let us try other models and see what happens 

DreamshaperXL Turbo has also two images reference but the differences is less important 


Trying different model show me that the model with few setps I used is different from other models and explain this differences. 


Let see what we have with clipvision and sdxl base model 





Prompt injection can be a key changer, giving us better control over the final image and designing what is more important or dominant. Without input 8, middle and output will be applied on the first reference. 









