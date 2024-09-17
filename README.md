# 🔗 Comfyui : Bjornulf_custom_nodes v0.36 🔗

# ❤️ Coffee : ☕☕☕☕☕ 5/5

https://ko-fi.com/bjornulf

# ☁ Usage in cloud : 

If you want to use my nodes and comfyui in the cloud, I'm managing an optimized template on runpod : <https://runpod.io/console/deploy?template=r32dtr35u1&ref=tkowk7g5>  
Template name : `bjornulf-comfyui-allin-workspace`, can be operational in ~3 minutes. (Depending on your pod)  
You need to create and select a network volume before using that, size is up to you, i have 50Gb Storage because i use cloud only for Flux or lora training on a 4090. (~0.7$/hour)  
⚠️ When pod is ready, you need to open a terminal in browser (After clicking on `connect` from your pod) and use this to launch ComfyUI manually : `cd /workspace/ComfyUI && python main.py --listen 0.0.0.0 --port 3000` (Much better to control it with a terminal, check logs, etc...)  
After that you can just click on the `Connect to port 3000` button.  
As file manager, you can use the included `JupyterLab` on port 8888.  
If you have any issues with it, please let me know.  
For me : I have a computer with 4070 super with 12Gb and flux fp8 simple wokflow is about ~40 seconds. With a 4090 in the cloud I can run flux fp16 in ~12 seconds.  
It will manage everything in Runpod network storage (`/workspace/ComfyUI`), so you can stop and start the cloud GPU without losing anything, change GPU or whatever.  
Zone : I recommend `EU-RO-1`, but up to you.  
Top-up your Runpod account with minimum 10$ to start.  
⚠️ Warning, you will pay by the minute, so not recommended for testing or learning comfyui. Do that locally !!!  
Run cloud GPU only when you already have your workflow ready to run.  
Advice : take a cheap GPU for testing, downloading models or settings things up.  
To download checkpoint or anything else, you need to use the terminal.  
For downloading from Huggingface (get token here <https://huggingface.co/settings/tokens>).  
Here is example for everything you need for flux dev :  
```
huggingface-cli login --token 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
huggingface-cli download black-forest-labs/FLUX.1-dev flux1-dev.safetensors --local-dir /workspace/ComfyUI/models/unet
huggingface-cli download comfyanonymous/flux_text_encoders clip_l.safetensors --local-dir /workspace/ComfyUI/models/clip
huggingface-cli download comfyanonymous/flux_text_encoders t5xxl_fp16.safetensors --local-dir /workspace/ComfyUI/models/clip
huggingface-cli download black-forest-labs/FLUX.1-dev ae.safetensors --local-dir /workspace/ComfyUI/models/vae
```
To use Flux you can just drag and drop in your browser the .json from my github repo : `workflows/FLUX_dev_troll.json`, direct link : <https://github.com/justUmen/ComfyUI-BjornulfNodes/blob/main/workflows/FLUX_dev_troll.json>.  

For downloading from civitai (get token here <https://civitai.com/user/account>), just copy/paste the link of checkpoint you want to download and use something like that, with your token in URL :  
```
CIVITAI="8b275fada679ba5812b3da2bf35016f6"
wget --content-disposition -P /workspace/ComfyUI/models/checkpoints "https://civitai.com/api/download/models/272376?type=Model&format=SafeTensor&size=pruned&fp=fp16&token=$CIVITAI"
```

# Dependencies

- `pip install ollama` (you can also install ollama if you want :  https://ollama.com/download) - You don't need to really install it if you don't want to use my ollama node. (BUT you need to run `pip install ollama`)
- `pip install pydub` (for TTS node)

# 📝 Changelog

- **v0.2**: Improve ollama node with system prompt + model selection.
- **v0.3**: Add a new node : Save image to a chosen folder.
- **v0.3**: Add comfyui Metadata / workflow to all my image-related nodes.
- **v0.4**: Support transparency option with webm format, options encoders. As well as input for audio stream. 
- **v0.5**: New node : Remove image transparency (alpha) - Fill alpha channel with solid color.
- **v0.5**: New node : Image to grayscale (black & white) - Convert an image to grayscale.
- **v0.6**: New node : Combine images (Background + Overlay) - Combine two images into a single image.
- **v0.7**: Replace Save API node with Save Bjornulf Lobechat node. (For my custom lobe-chat)
- **v0.8**: Combine images : add an option to put image top, bottom or center.
- **v0.8**: Combine texts : add option for slashes /
- **v0.8**: Add basic node to transform greenscreen in to transparency.
- **v0.9**: Add a new node : Return one random line from input.
- **v0.10**: Add a new node : Loop (All Lines from input) - Iterate over all lines from an input text.
- **v0.11**: Add a new node : Text with random Seed - Generate a random seed, along with text.
- **v0.12**: Combine images : Add option to move vertically and horizontally. (from -50% to 150%)
- **v0.13**: Add a new node: Load image with transparency (alpha) - Load an image with transparency.
- **v0.14**: Add a new node: Cut image from a mask
- **v0.15**: Add two new nodes: TTS - Text to Speech and Character Description Generator
- **v0.16**: Big changes on Character Description Generator
- **v0.17**: New loop node, combine by lines.
- **v0.18**: New loop node, Free VRAM hack
- **v0.19**: Changes for save to folder node : ignore missing images filenames, will use the highest number found + 1.
- **v0.20**: Changes for lobechat save image : include the code of free VRAM hack + ignore missing images filenames
- **v0.21**: Add a new write text node that also display the text in the comfyui console (good for debugging)
- **v0.22**: Allow write text node to use random selection like this {hood|helmet} will randomly choose between hood or helmet.
- **v0.23**: Add a new node: Pause, resume or stop workflow.
- **v0.24**: Add a new node: Pause, select input, pick one.
- **v0.25**: Two new nodes: Loop Images and Random image.
- **v0.26**: New node : Loop write Text. Also increase nb of inputs allowed for most nodes. (+ update some breaking changes)
- **v0.27**: Two new nodes : Loop (Model+Clip+Vae) and Random (Model+Clip+Vae) - aka Checkpoint / Model
- **v0.28**: Fix random texts and add a lot of screenshots examples for several nodes.
- **v0.29**: Fix floating points issues with loop float node.
- **v0.30**: Update the basic Loop node with optional input.
- **v0.31**: ❗Sorry, Breaking changes for Write/Show text nodes, cleaner system : 1 simple write text and the other is 1 advanced with console and special syntax. Also Show can now manage INT, FLOAT, TEXT.
- **v0.32**: Quick rename to avoid breaking loop_text node.
- **v0.33**: Control random on paused nodes, fix pydub sound bug permissions on Windows.
- **v0.34**: Two new nodes : Load Images from output folder and Select an Image, Pick.
- **v0.35**: Great improvements of the TTS node 31. It will also save the audio file in the "ComfyUI/Bjornulf_TTS/" folder. - Not tested on windows yet -
- **v0.36**: Fix random model.

# 📝 Nodes descriptions

## 1 - 👁 Show (Text, Int, Float)

![Show Text](screenshots/show.png)

**Description:**  
The show node will only display text, or a list of several texts. (read only node)  
3 types are managed : Green is for STRING type, Orange is for FLOAT type and blue is for INT type. I put colors so I/you don't try to edit them. 🤣  

## 2 - ✒ Write Text

![write Text](screenshots/write.png)

**Description:**  
Simple node to write text.  

## 3 - ✒🗔 Advanced Write Text

![write Text Advanced](screenshots/write_advanced.png)

**Description:**  
Advanced Write Text node allows for special syntax to accept random variants, like `{hood|helmet}` will randomly choose between hood or helmet.  
You also have `seed` and `control_after_generate` to manage the randomness.  
It is also displaying the text in the comfyui console. (Useful for debugging)  
Example of console logs :  
```
Raw text: photo of a {green|blue|red|orange|yellow} {cat|rat|house}
Picked text: photo of a green house
```

## 4 - 🔗 Combine Texts
![Combine Texts](screenshots/combine_texts.png)

**Description:**  
Combine multiple text inputs into a single output. (can have separation with : comma, space, new line or nothing.)

## 5 - 🎲 Random (Texts)
![Random Text](screenshots/random_text.png)

**Description:**  
Generate and display random text from a predefined list. Great for creating random prompts.  
You also have `control_after_generate` to manage the randomness.  

## 6 - ♻ Loop
![Loop](screenshots/loop.png)

**Description:**  
General-purpose loop node, you can connect that in between anything.  
It has an optional input, if no input is given, it will loop over the value of the STRING "if_no_input" (take you can edit).  
❗ Careful this node accept everything as input and output, so you can use it with texts, integers, images, mask, segs etc... but be consistent with your inputs/outputs.  
Do not use this Loop if you can do otherwise.  

This is an example together with my node 28, to force a different seed for each iteration :   
![Loop](screenshots/loop4.png)

## 7 - ♻ Loop Texts
![Loop Texts](screenshots/loop_texts.png)

**Description:**  
Cycle through a list of text inputs.  

Here is an example of usage with combine texts and flux :  
![Loop Texts example](screenshots/loop_text_example.png)

## 8 - ♻ Loop Integer
![Loop Integer](screenshots/loop_integer.png)
![Loop Int + Show Text](screenshots/loop_int+show_text.png)

**Description:**  
Iterate through a range of integer values, good for `steps` in ksampler, etc...

❗ Don't forget that you can convert ksampler widgets to input by right-clicking the ksampler node :  
![Widget to Input](screenshots/widget-to-input.png)

Here is an example of usage with ksampler (Notice that with "steps" this node isn't optimized, but good enough for quick testing.) :  
![Widget to Input](screenshots/example_loop_integer.png)

## 9 - ♻ Loop Float
![Loop Float + Show Text](screenshots/loop_float+show_text.png)
![Loop Float](screenshots/loop_float.png)

**Description:**  
Loop through a range of floating-point numbers, good for `cfg`, `denoise`, etc...  

Here is an example with controlnet, trying to make a red cat based on a blue rabbit :  
![Loop All Samplers](screenshots/loop_float_example.png)

## 10 - ♻ Loop All Samplers
![Loop All Samplers](screenshots/loop_all_samplers.png)

**Description:**  
Iterate over all available samplers to apply them sequentially. Ideal for testing.  

Here is an example of looping over all the samplers with the normal scheduler :  
![Loop All Samplers](screenshots/example_loop_all_samplers.png)

## 11 - ♻ Loop All Schedulers
![Loop All Schedulers](screenshots/loop_all_schedulers.png)

**Description:**  
Iterate over all available schedulers to apply them sequentially. Ideal for testing. (same idea as sampler above, but for schedulers)  

## 12 - ♻ Loop Combos
![Loop Combos](screenshots/loop_combos.png)

**Description:**  
Generate a loop from a list of my own custom combinations (scheduler+sampler), or select one combo manually.  
Good for testing.

Example of usage to see the differences between different combinations :    
![example combos](screenshots/example_combos.png)

## 13/14 - 📏 + 🖼 Resize and Save Exact name ⚠️💣
![Resize and Save Exact](screenshots/resize_save_exact.png)

**Description:**  
Resize an image to exact dimensions. The other node will save the image to the exact path.  
⚠️💣 Warning : The image will be overwritten if it already exists.

## 15 - 💾 Save Text
![Save Text](screenshots/save_text.png)

**Description:**  
Save the given text input to a file. Useful for logging and storing text data.

## 16 - 🖼💬 Save image for Bjornulf LobeChat (❗For my custom [lobe-chat](https://github.com/justUmen/Bjornulf_lobe-chat)❗)
![Save Bjornulf Lobechat](screenshots/save_bjornulf_lobechat.png)

**Description:**  
❓ I made that node for my custom lobe-chat to send+receive images from Comfyui API : [lobe-chat](https://github.com/justUmen/Bjornulf_lobe-chat)  
It will save the image in the folder `output/BJORNULF_LOBECHAT/`. 
The name will start at `api_00001.png`, then `api_00002.png`, etc...  
It will also create a link to the last generated image at the location `output/BJORNULF_API_LAST_IMAGE.png`.  
This link will be used by my custom lobe-chat to copy the image inside the lobe-chat project.  

## 17 - 🖼 Save image as `tmp_api.png` Temporary API ⚠️💣
![Save Temporary API](screenshots/save_tmp_api.png)

**Description:**  
Save image for short-term use : ./output/tmp_api.png ⚠️💣  

## 18 - 🖼📁 Save image to a chosen folder name
![Save Temporary API](screenshots/save_image_to_folder.png)

**Description:**  
Save image in a specific folder : `my_folder/00001.png`, `my_folder/00002.png`, etc...  
Also allow multiple nested folders, like for example : `animal/dog/small`.

## 19 - 🦙 Ollama
![Show Text](screenshots/ollama.png)

**Description:**  
Will generate detailed text based of what you give it.  
I recommend using `mistral-nemo` if you can run it, but it's up to you. (Might have to tweak the system prompt a bit)  
⚠️ Warning : Having an ollama node that will run for each generation might be a bit heavy on your VRAM. Think about if you really need it or not.

## 20 - 📹 Video Ping Pong
![Video Ping Pong](screenshots/video_pingpong.png)

**Description:**  
Create a ping-pong effect from a list of images (from a video) by reversing the playback direction when reaching the last frame. Good for an "infinity loop" effect.

## 21 - 📹 Images to Video
![Images to Video](screenshots/imgs2video.png)

**Description:**  
Combine a sequence of images into a video file.  
❓ I made this node because it supports transparency with webm format. (Needed for rembg)  
Temporary images are stored in the folder `ComfyUI/temp_images_imgs2video/` as well as the wav audio file.

## 22 - 🔲 Remove image Transparency (alpha)
![Remove Alpha](screenshots/remove_alpha.png)

**Description:**  
Remove transparency from an image by filling the alpha channel with a solid color. (black, white or greenscreen)  
Of course it takes in an image with transparency, like from rembg nodes.  
Necessary for some nodes that don't support transparency.  

## 23 - 🔲 Image to grayscale (black & white)
![Image to Grayscale](screenshots/grayscale.png)

**Description:**  
Convert an image to grayscale (black & white)  
Example : I sometimes use it with Ipadapter to disable color influence.  
But you can sometimes also want a black and white image... 

## 24 - 🖼+🖼 Combine images (Background + Overlay)
![Combine Images](screenshots/combine_background_overlay.png)

**Description:**  
Combine two images into a single image : a background and one (or several) transparent overlay. (allow to have a video there, just send all the frames and recombine them after.)  
Update 0.11 : Add option to move vertically and horizontally. (from -50% to 150%)  
❗ Warning : For now, `background` is a static image. (I will allow video there later too.)  
⚠️ Warning : If you want to directly load the image with transparency, use my node `🖼 Load Image with Transparency ▢` instead of the `Load Image` node.  

## 25 - 🟩➜▢ Green Screen to Transparency
![Greenscreen to Transparency](screenshots/greeenscreen_to_transparency.png)

**Description:**  
Transform greenscreen into transparency.  
Need clean greenscreen ofc. (Can adjust threshold but very basic node.)

## 26 - 🎲 Random line from input
![Random line from input](screenshots/random_line_from_input.png)

**Description:**  
Take a random line from an input text. (When using multiple "Write Text" nodes is annoying for example, you can use that and just copy/paste a list from outside.)  
You can change fixed/randomize for `control_after_generate` to have a different text each time you run the workflow. (or not)  

## 27 - ♻ Loop (All Lines from input)
![Loop input](screenshots/loop_all_lines.png)

**Description:**  
Iterate over all lines from an input text. (Good for testing multiple lines of text.)

## 28 - 🔢 Text with random Seed

**Description:**  

❗ This node is used to force to generate a random seed, along with text.  
But what does that mean ???  
When you use a loop (♻), the loop will use the same seed for each iteration. (That is the point, it will keep the same seed to compare results.)  
Even with `randomize` for `control_after_generate`, it is still using the same seed for every loop, it will change it only when the workflow is done.  
Simple example without using random seed node : (Both images have different prompt, but same seed)  

![Text with random Seed 1](screenshots/random_seed_1.png)

So if you want to force using another seed for each iteration, you can use this node in the middle.
For example, if you want to generate a different image every time. (aka : You use loop nodes not to compare or test results but to generate multiple images.)  
Use it like that for example : (Both images have different prompt AND different seed)  

![Text with random Seed 2](screenshots/random_seed_2.png)

Here is an example of the similarities that you want to avoid with FLUX with different prompt (hood/helmet) but same seed :

![Text with random Seed 3](screenshots/random_seed_3_flux.png)

Here is an example of the similarities that you want to avoid with SDXL with different prompt (blue/red) but same seed :

![Text with random Seed 4](screenshots/random_seed_4_sdxl.png)

FLUX : Here is an example of 4 images without Random Seed node on the left, and on the right 4 images with Random Seed node :

![Text with random Seed 5](screenshots/result_random_seed.png)

## 29 - 🖼 Load Image with Transparency ▢
![Load image Alpha](screenshots/load_image_alpha.png)

**Description:**  
Load an image with transparency.  
The default `Load Image` node will not load the transparency.  

## 30 - 🖼✂ Cut image with a mask
![Cut image](screenshots/image_mask_cut.png)

**Description:**  
Cut an image from a mask.  

## 31 - 🔊 TTS - Text to Speech (100% local, any voice you want, any language)
![TTS](screenshots/tts.png)

**Description:**  
[Listen to the audio example](https://github.com/user-attachments/assets/5a4a67ff-cf70-4092-8f3b-1ccc8023d8c6)

❗ Node never tested on windows, only on linux for now. ❗  

Use my TTS server to generate speech from text, based on XTTS v2.  
❗ Of course to use this comfyui node (frontend) you need to use my TTS server (backend) : <https://github.com/justUmen/Bjornulf_XTTS>  
I made this backend for <https://github.com/justUmen/Bjornulf_lobe-chat>, but you can use it with comfyui too with this node.  
After having `Bjornulf_XTTS` installed, you NEED to create a link in my Comfyui custom node folder called `speakers` : `ComfyUI/custom_nodes/Bjornulf_custom_nodes/speakers`  
That link must be a link to the folder where you installed/stored the voice samples you use for my TTS, like `default.wav`.  
If my TTS server is running on port 8020 (You can test in browser with the link <http://localhost:8020/tts_stream?language=en&speaker_wav=default&text=Hello>) and voice samples are good, you can use this node to generate speech from text.  

**Details**  
This node should always be connected to a core node : `Preview audio`.  

My node will generate and save the audio files in the `ComfyUI/Bjornulf_TTS/` folder, followed by the language selected, the name of the voice sample, and the text.  
Example of audio file from the screenshot above : `ComfyUI/Bjornulf_TTS/Chinese/default.wav/你吃了吗.wav`  
You can notice that you don't NEED to select a chinese voice to speak chinese. Yes it will work, you can record yourself and make yourself speak whatever language you want.  
Also, when you select a voice with this format `fr/fake_Bjornulf.wav`, it will create an extra folder `fr` of course. : `ComfyUI/Bjornulf_TTS/English/fr/fake_Bjornulf.wav/hello_im_me.wav`. Easy to see that you are using a french voice sample for an english recording.  

`control_after_generate` as usual, it is used to force the node to rerun for every workflow run. (Even if there is no modification of the node or its inputs.)  
`overwrite` is used to overwrite the audio file if it already exists. (For example if you don't like the generation, just set overwrite to True and run the workflow again, until you have a good result. After you can set it to back to False. (Paraphrasing : without overwrite set to True, It won't generate the audio file again if it already exists in the `Bjornulf_TTS` folder.)  
`autoplay` is used to play the audio file inside the node when it is executed. (Manual replay or save is done in the `preview audio` node.)  

So... note that if you know you have an audio file ready to play, you can still use my node but you do NOT need my TTS server to be running.
My node will just play the audio file if it can find it, won't try to connect th backend TTS server.  
Let's say you already use this node to create an audio file saying `workflow is done` with the Attenborough voice  :
![TTS](screenshots/tts_end.png)  

As long as you keep exactly the same settings, it will not use my server to play the audio file! You can safely turn in off, so it won't use your precious VRAM Duh. (TTS server should be using ~3GB of VRAM.)  

Also input is optional, it means that you can make a workflow with ONLY my TTS node to pre-generate the audio files with the sentences you want to maybe use later, example :  
![TTS](screenshots/tts_generate.png)  

### 32 - 🧑📝 Character Description Generator
![characters](screenshots/characters.png)
![characters](screenshots/characters2.png)

**Description:**  
Generate a character description based on a json file in the folder `characters` : `ComfyUI/custom_nodes/Bjornulf_custom_nodes/characters`  
Make your own json file with your own characters, and use this node to generate a description.  
❗ For now it's very basic node, a lot of things are going to be added and changed !!!  
Some details are unusable for some checkpoints, very much a work in progress, the json structure isn't set in stone either.  
Some characters are included.  

### 33 - ♻ Loop (All Lines from input 🔗 combine by lines)

![loop combined](screenshots/loop_combined.png)

**Description:**  
Sometimes you want to loop over several inputs but you also want to separate different lines of your output.  
So with this node, you can have the number of inputs and outputs you want. See example for usage.  

### 34 - 🧹 Free VRAM hack
![free vram](screenshots/free_vram_hack1.png)
![free vram](screenshots/free_vram_hack2.png)

**Description:**  
So this is my attempt at freeing up VRAM after usage, I will try to improve that.  
For me, on launch ComfyUI is using 180MB of VRAM, after my clean up VRAM node it can go back down to 376MB.  
I don't think there is a clean way to do that, so I'm using a hacky way.  
So, not perfect but better than being stuck at 6GB of VRAM used if I know I won't be using it again...  
Just connect this node with your workflow, it takes an image as input and return the same image without any changes.  
❗ Comfyui is using cache to run faster (like not reloading checkpoints), so only use this free VRAM node when you need it.  
❗ For this node to work properly, you need to enable the dev/api mode in ComfyUI. (You can do that in the settings)  

### 35 - ⏸️ Paused. Resume or Stop ?

![pause resume stop](screenshots/pause1.png)
![pause resume stop](screenshots/pause2.png)
![pause resume stop](screenshots/pause3.png)

**Description:**  
Automatically pause the workflow, and rings a bell when it does. (play the audio `bell.m4a` file provided)  
You can then manually resume or stop the workflow by clicking on the node's buttons.  
I do that let's say for example if I have a very long upscaling process, I can check if the input is good before continuing. Sometimes I might stop the workflow and restart it with another seed.  
You can connect any type of node to the pause node, above is an example with text, but you can send an IMAGE or whatever else, in the node `input = output`. (Of course you need to send the output to something that has the correct format...)  

### 36 - ⏸️🔍 Paused. Select input, Pick one

![pick input](screenshots/pick.png)

**Description:**  
Automatically pause the workflow, and rings a bell when it does. (play the audio `bell.m4a` file provided)  
You can then manually select the input you want to use, and resume the workflow with it.  
You can connect this node to anything you want, above is an example with IMAGE. But you can pick whatever you want, in the node `input = output`.  

### 37 - 🎲🖼 Random Image

![random image](screenshots/random_image.png)

**Description:**  
Just take a random image from a list of images.  

### 38 - ♻🖼 Loop (Images)

![loop images](screenshots/loop_images.png)

**Description:**  
Loop over a list of images.  
Usage example : You have a list of images, and you want to apply the same process to all of them.  
Above is an example of the loop images node sending them to an Ipadapter workflow. (Same seed of course.)  

### 39 - ♻ Loop (✒🗔 Advanced Write Text)

![loop write text](screenshots/loop_write_text.png)

**Description:**  
If you need a quick loop but you don't want something too complex with a loop node, you can use this combined write text + loop.  
It will take the same special syntax as the Advanced write text node `{blue|red}`, but it will loop over ALL the possibilities instead of taking one at random.  

### 40 - 🎲 Random (Model+Clip+Vae) - aka Checkpoint / Model

![pick input](screenshots/random_checkpoint.png)

**Description:**  
Just take a trio at random from a load checkpoint node.  

### 41 - ♻ Loop (Model+Clip+Vae) - aka Checkpoint / Model

![pick input](screenshots/loop_checkpoint.png)

**Description:**  
Loop over all the trios from several checkpoint node.  

### 42 - 📂🖼 Load Images from output folder

![pick input](screenshots/load_images_folder.png)

**Description:**  
Quickly select all images from a folder inside the output folder. (Not recursively.)  
So... As you can see from the screenshot the images are split based on their resolution.  
It is not a choice I made, it is something that is part of the comfyui environment.  
It's also not possible to edit dynamically the number of outputs, so I just picked a number : 4.  
The node will separate the images based on their resolution, so with this node you can have 4 different resolutions per folder. (If you have more than that, maybe you should have another folder...)  
To avoid error or crash if you have less than 4 resolutions in a folder, the node will just output white tensors. (white square image.)  
So this node is a little hacky for now, but i can select my different characters in less than a second.  
If you want to know how i personnaly save my images for a specific character, here is part of my workflow (Notice that i personnaly use / for folders because I'm on linux) :  
![pick input](screenshots/character_save.png)  
In this example I put "character/" as a string and then combine with "nothing". But it's the same if you do "character" and then combine with "/". (I just like having a / at the end of my folder's name...)  

If you are satisfied with this logic, you can then select all these nodes, right click and `Convert to Group Node`, you can then have your own customized "save character node" :  
![pick input](screenshots/bjornulf_save_character_group.png)

Here is another example of the same thing but excluding the save folder node :  
![pick input](screenshots/bjornulf_save_character_group2.png)

### 43 - 🖼🔍 Select an Image, Pick

![pick input](screenshots/select_image.png)

**Description:**  
Select an image from a list of images.  
Useful in combination with my Load images from folder and preview image nodes.  

You can also of course make a group node, like this one, which is the same as the screenshot above :  
![pick input](screenshots/select_image_group.png)