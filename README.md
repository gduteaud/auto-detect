# AutoDetect

A couple of weeks ago now, OpenAI introduced image generation functionality to its flagship GPT-4o model, and by the following weekend it felt like the only thing everyone was talking about.

That same weekend, a LinkedIn post caught my eye: highly realistic, 4o-generated images of a receipt and a vandalized car captioned with something about how this capability could facilitate insurance fraud. Whoever made that post, if you are reading this, I apologize for not giving you proper attribution - unfortunately, LinkedIn's search functionality being so utterly terrible, I am now unable to find that post again.

Anyway - that got me thinking and I was curious to see if I could replicate something similar, so I went to ChatGPT to try it myself. Lo and behold, this is what I got on my first attempt:

![](/data/fake/0.png)

I couldn't believe my eyes. Nearly perfect, save for a handful of subtle tells (like the emblem). I gave it another go, with a slightly improved prompt:

![](/data/fake/1.png)

Even closer to perfect, if not for the absence of a license plate. As I generated more and more images over the next few days it became clear that this could successfully fool someone. Maybe not a professional insurance adjuster in this incarnation, but certainly not that far off.

## The challenge

I don't think I need to go into why fraud is bad (hint: bad actors make everyone else's rates go up). Insurance companies dedicate enormous resources to combatting fraudulent claims, and I'm sure that already includes tools to detect fake images. Still, it's by definition an open problem due to the cat-and-mouse game inherent to fake image detection. Fakers are always one step ahead, because detection models can always be leveraged to develop generation models good enough to defeat them (see [GANs](https://en.wikipedia.org/wiki/Generative_adversarial_network)). Detection models can in turn be further improved (assuming enough high-quality fakes from the latest generation models can be identified in order to serve as training data), leading to yet more performant generation models, and so on *ad vitam aeternam*.

## Limitations

Right now, rate limiting on GPT-4o's image generation feature, and the lack of a corresponding API, are a major bottleneck for this project. Crowdsourcing might be an option to help overcome this (see "next steps" section below).

More generally, data availability is a fundamental limitation for an amateur initiative like this, compared to the vast amount of data collected by insurance companies over decades.

## Next steps

- I would like to turn this into a collaborative project with a simple web UI to allow volunteer contributors to submit both fake and real images, which would then be fed into an automated training pipeline
- Once enough data has been collected in this way I would also like to set up a GAN to see both how good we can get these kinds of fakes, and how good we can get at detecting them

## Notes
- The provided notebook is intended to be run in Google Colab as it includes a few bits of Colab-specific code, but should easy to adapt to any other environment (a GPU is strongly recommended).
- I am intentionally not sharing the prompts I used to generate those fake images as I feel that would be irresponsible. If you are interested in collaborating on this project, please reach out.

## Usage
1. Open the notebook in Colab and run the cells, including uploading the zipped data. The zip is rather large and so takes a while to load.
2. Use the last cell to upload a validation image of your choice, either among those provided in the validation folder or your own. 

## Model
- Architecture: resnet18
- Input size: 224 x 224
- Classes: 2 (real, fake)
