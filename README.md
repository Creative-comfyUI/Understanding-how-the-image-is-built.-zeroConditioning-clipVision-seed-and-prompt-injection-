<h1>Understanding how the image is built. zeroConditioning, clipVision, seed and prompt injection </h1>

Are we sure we understand how the image is built and what reference the prompt image is based on?

Since [@cubiq](https://github.com/cubiq/prompt_injection) creation of the prompt injection node, I have discovered that what I thought about image creation in comfyUI is probably not what I imagined.  

Before I begin my demonstration. I invite you to read the first part of Prompt Injection (https://github.com/Creative-comfyUI/prompt_injection) . You can also read what I have written about seeds (https://github.com/Creative-comfyUI/seed_eng). All this information is necessary to understand what I am about to demonstrate. 

In my previous repisotery about prompt injection, <b>I explained that even prompt is muted with zeroConditioning, ksampler generated image </b>. <b>This image looks like a reference</b>. You have to understand that no text in the <i>clip text encode</i> doesn't mean that the prompt is muted. The zeroConditioning ensures that no text information is used by the clip (https://openai.com/index/clip/). 

The image generated by zeroConditioning appears to be a reference image, but how it is used is the question. It is probably the noise that is used.  What we are sure of is that for each seed the model produces an image, even without a prompt. For the same seed, there is a similarity between the images rendered (example: a man, a room, a garden.... ) but not always. What surprised me was that each model didn't give the same finishing touch to the image reference, some are blured, some are not well defined and others are a perfect photo. Let us look at a few examples with the same seeds and zero conditioning. 

![Model_Euler](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/c7580084-e179-4160-96f2-d81d6b5ef9f2)

The most intriguing is that the sampler can give a different image. Many users thought that the sampler influenced the finishing of the image. Sampler can influence much more the images. Lets have a look at some example with always zeroConditioning and same seed. 

![Sampler](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/62accb8d-e2e4-49f3-b6c2-31066a05e182)

There is another surprise the format can change the reference image too 

![Size](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/dbfa819e-6cff-4ea2-9521-9554b758c4ca)

Now let us use prompt injection to see what has happened. As I mentioned in my previous repository, input 8 is the key change of the image. Not for the first image, but for the third more than the second. Input 8 with an empty prompt affected the result. The most defined reference image will show the more important change. Example with Sdxl 1 the change is slight.  Let us look at some examples. 

This example is with sdxl_ligthning_8step model 

![Screenshot 2024-06-16 at 2 38 21 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/675859cc-039f-4901-837b-434a8feddae0)

If we change the size to 832 * 1216 the third image is completely different, which is not the case when using Euler. Input 8 change the image 

![Screenshot 2024-06-16 at 2 45 07 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/73b2d6c1-eead-42df-9c25-975a18ba0b9a)

Before continuing, I write a prompt and mute the negative prompt to see what the result is for each model without prompt injection. 

Prompt : Paris champ de mars, an elegant woman colorfull, in 1950 style

![Model_Prompt](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/6f8d9009-6671-4b81-8c8d-1497a41930fb)

Now let try If, as previously, sampler change the image. I am going to use the same model and the same samplers I used before and see the results 

![Sampler_Prompt](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/b57a2672-eef1-4469-8ef7-aceb2f0efc30)

The results obtained with different samplers show us that the image is in relation to the reference image style (realistic, drawing, sketching...) but it is not always the case 

All these images are in 1024 * 1024 format, which means that with another format the result will be different. 

w 832 * h 1216 

![Screenshot 2024-06-16 at 7 18 29 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/09ce416b-0b76-4a12-a8a1-c9a1333e8322)

w 1536 * 640 

![Screenshot 2024-06-16 at 7 43 30 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/3ba7bfa5-c599-47af-9eb7-57e5714d0485)

Times to times with bigger images we can see a signature on the image or text as with this image without being able to read it. 

What is commun with all these images ? 

The Eiffel Tower, because it is associated with the Champ de Mars in Paris, cars, an elegant lady in a hat and, finally, nice colours. 

Before continuing the explanation, we can conclude that Euler samplers always give the same images. Other samplers may give different images or style. The image following the first image can be different from the others with samplers other than Euler. The first picture is a kind of reference. The seed is linked to this image. Changing the size of the image changes the point of view and can change the image. It looks like the image size is related to the deep field of the camera. 1526 * 640 can be considered as f22. 

Now we are going to use prompt injection as it can change many things in the result of the image. 

Adding an empty prompt to output 8 add variation to image 2 and 3. 3 has much more variation. Image 1 didn't change 

![Screenshot 2024-06-16 at 8 30 33 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/898e50ab-2f50-4c7b-8a49-c40a75c0e8fa)

Now I will go to the muted prompt and write the prompt in the one that links to output 8 

![Screenshot 2024-06-16 at 10 58 17 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/13363592-3f64-4a93-897d-0efebea52597)

This means that the apply prompt in input 8 doesn't create an image, but gives a variation of the image reference, because images 2 and 3 are different. Input 8 will create a variation no matter what you write. This means that if you have a good reference image you can use it to make a variation using input 8  and using batch size 3, depending on the model and latent size the variation may be less important and less or more interesting. Output 0 and 1 will help to add detail to these variations. Let us take a look at the previous examples using the DreamshaperXL mode and the LCM sampler. I use zeroconditionning for the prompt and the input 8 prompt is blank here is the result 

![LCM input_8](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/488c4ac4-0809-4ffb-833e-228aa1e470bc)

Now I am going to add details to image 2 and 3 using different input and ouput 

input 5 and input 8 with blank prompt change face expression of the third image 

![visage](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/ed8edfa3-2ea5-4117-8bb9-5c057a9a1d36)

input 7  and input 8 with blank prompt change much more face expression of the third image 

![visage2](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/ef3d2c02-52a1-4c18-bd99-1f14b8f6f460)

Now we are going to use prompt with input 0 and input 1 

input 0 : woman smiling and dancing with hands up
input 1 : Red jacket, blue trouser, yellow hat, 

![Screenshot 2024-06-17 at 8 23 33 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/7e7167c1-7a46-4484-a0d0-58231cb79ee0)

Now I will link prompt injection all to a prompt. The prompt is the one we use before : Paris champ de mars, an elegant woman colourful, in 1950 style
This prompt changes the second image, but the prompt was not applied. If we disconnect input 8 and keep all outputs 1 and 0, then not only the third image but also the second one will be affected. 
This time the output prompt 0 and 1 are correctly applied, but it is not the prompt we expected.

![Screenshot 2024-06-17 at 8 42 13 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/4e6cf9d0-8249-47fe-a7a5-574f26500d34) ![Screenshot 2024-06-17 at 10 09 27 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/5a9a373a-c3c3-40e4-8319-c0d8b7612ea6)

If we now change the Lcm sampler for dpmpp_2m with input 8, the result is different. The second image is the metamorphosis of the reference image and the third image is the final transformation. 

![Screenshot 2024-06-17 at 9 25 10 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/fd6106ab-def8-4c7a-9c4c-4ecc424b042c)

Now we applied the current prompt and prompt injection all, output 0 and output 1 applied

![Screenshot 2024-06-17 at 10 23 57 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/22203c2c-91f5-4173-9ad5-e011486c2ad9) 

without injection all

![Screenshot 2024-06-17 at 9 57 39 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/573ab13b-4124-4e08-90b1-9d10963dad0e) 

without injection all and dpmmp_sde sampler instead Lcm 

![Screenshot 2024-06-17 at 10 42 38 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/9b9b2a50-f151-4754-bd94-7d01b1fefd7f)

Prompt injection bring precision and detail to the image. Adding input 8 blocked a part of the original prompt 

![Screenshot 2024-06-17 at 11 03 25 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/1080f954-1d40-4ac1-93d0-afc7f2ef3c56)

Two points: Using an image for latent_image instead of empty latent changes the posture of the character. Using batch size 1 can give a different result than if we choose batch size 3. 

The question is: is there a relationship between the reference image and the final image, or is it a glitch ? Is the reference image, an AI image or an existing image that was used to train the AI? 

There is a relationship between the reference image with the seed for sure. That means there is a relationship also with the image we will create especially with the first image 

Now let use clip vision to confirm or not this relationship. Clipvision let us used an image as prompt. Using this technic can help us to mix two images and create a new one. Let try and see what happend. It is important to understand that it looks like the model we used seems to affect the result. Some models seem to be more accurate than others. Why is another question? 

Let us look at some examples.

<h3> Model DreamShaperXL Turbo </h3> 

Regular image with prompt 

![RenduDreamShaper](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/99279efb-0228-46f0-8f56-ad254594bce7)

Image with muted prompt (zeroconditionning) 

![Dream_muted](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/ecb0eaa1-a5d0-4e9d-93bd-84f52706ca8c)

Image using clip vision zeroconditionning 

Strength 0 

![ClipVisionDreamShapter](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/e6798b1f-609b-4f00-ba46-0502ff2f4ee9)

Strength 1 

![Clipvision1_dreamShaper](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/387ead0d-afc7-4ac5-b74c-4870e0795bb9)

For strength 1, I wonder where this picture came from. It looks like a variation of the first image. Playing with the strength is not a variation between strength 0 and 1, it looks like a variation of strength 1. 

This happend because we choose image reference 1. If we choose the third image of our batch size everything is different with strength 1 

![Screenshot 2024-06-18 at 5 01 47 PM](https://github.com/Creative-comfyUI/Understanding-how-the-image-is-built.-zeroConditioning-clipVision-seed-and-prompt-injection-/assets/166729777/27a798b0-86c2-417b-a409-46b0f5d8b86a)


What happens if we vary the seed?

The new seed will give a new reference image for strength 0, meaning the image doesn't contain the image reference. The reference is linked to the seed. 

Now we are going to use another model, which seems to be different and maybe more accurate.  I invite to read the previous repositery on the pormpt injection

With the model sdxl_lightning_8 steps we will have for strength 0 the reference image and for 1 the third image if have had with input 8 with prompt zeroconditionning 

This model as you can see in the previous repository seems to act differently. Using batch size 1 will give the image 3 of batch size 3. For this model there is two different reference. Why ? That is the question ? 

For the same seed, with the same model, the reference image will always be the same. Using clip vision with this model and image done with another model will give the same reference image but with variation. The sampler can influence the reference image Euler, LCM dpmmpp_.... or dpmpp_sde can have different references. 

Prompt injection can help us to add some detail more precisely wiht output 8. output 8 can in some case as seen with my previous repisotery on prompt injection help us to have variation of image reference and can give interesting result. In this case the choice of model is very important. Not all models react in the same way.

How is this reference used, how does it affect the result? Why is the effect important for some models and not for others?  If instead a model in Ksampler we can choose an image that will act differently at the one add in the latent, might be a good idea to see what happens?

Prompt injection can be a good tool if we can influence the results more precisely and decide what we want. At the same time, I haven't tested negative prompt, which can have an impact on the results describe in this text. 

This analysis was done to understand more what happens with the image and maybe it can give ideas to the developer to create new models or new nodes to have more control on the final image.











