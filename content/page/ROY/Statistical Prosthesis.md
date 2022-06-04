---
title: ROY/Statistical Prosthesis
tags:
categories:
date: 2022-05-29
lastMod: 2022-05-29
---




So First I started thinking about

training my own [[machine learning]] model with [[ml5]]

  + {{< youtube 8HEgeAbYphA >}}

  + Soon realized though this was a little broad, and I didn't know exactly how to apply this to all the text files I had generated

# [[chRNN]]

  + Then I looked into [Training a chRNN and using the model in ML5](https://github.com/ml5js/training-charRNN)

    + > RNNs work well when you want predict sequences or patterns from your inputs. Try to gather as much input text data as you can. The more the better. Compile all of the text data into a single text file and make note of where the file is stored (path) on your computer.

      + _(A quick tip to concatenate many small disparate _`.txt`_ files into one large training file: _`ls *.txt | xargs -L 1 cat >> input.txt`_)_ [[command line]]

      + Then essentially

```bash
$ git clone https://github.com/ml5js/training-charRNN
$ cd training-charRNN
$ pip install -r requirements.txt
$ python train.py --data_path /path/to/data/file.txt
```

      + When training is complete a JavaScript version of your model will be available in a folder called ./models (unless you specify a different path.)

      + Once the model is ready, you'll just need to point to it in your ml5 sketch, for more visit the charRNN() documentation.

```js
const charRNN = new ml5.charRNN('./models/your_new_model');
```

  + Started following this tutorial

    + {{< youtube nnhjvHYRsmM >}}

      + undefined [[python/virtualenv]]

        + For making isolated [[python]] environments.

          + Is this kinda like [[Node]]?

      + undefined `pip install virtualenv`

      + undefined `virtualenv ENV`

        + ENV is a placeholder for my workspace name

      + undefined once the environment is created, activate it with `source bin/activate`

        + ala `npm start`. but like specifies where python is running.

      + undefined the `(name)`

      + undefined `deactivate` deactivates the environment

      + undefined `virtualenv -p python3` specifies the version

      + undefined Recap

  + [[python/pip]]

    + installing a specific version with {{< logseq/mark >}} `pip install tensorflow{{< / logseq/mark >}}2.0.0`

    + upgrading pip `python -m pip install --upgrade pip setuptools`

  + In trying to install [[tensorflow]] I couldn't figure out how to get version 1.15.4. Not sure if that will be a problem...

![image.png](/assets/image_1645504110450_0.png)

      + Seems like it was....

    + Actually the real problem was not having [[python]] 3.6. Seems like tensorflow 1.15 is only supported on older version of python

    + Agh god why is it so hard to find python 3.6?!?!?

![image.png](/assets/image_1645505595953_0.png)

      + 

[[command line]]

after some real struggle bussing

OMG it is happening!

![image.png](/assets/image_1645507339695_0.png)



I plopped in the model to [[logseq]] with..... mixed results?

  + <div style="position: relative; padding-bottom: 168.05555555555557%; height: 0;"><iframe src="https://www.loom.com/embed/fe94126a49df44af9130374b108bfc09" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

  + 

I suppose that's all I really have the capacity for at the moment, but I'm interested to see where this goes.

Definitely seems like I need a much larger data-set or a more specific model. One that understands pages and the structure of the program a little better.

Some good gems

  + I am feeling happy right now

    + " to a self seetable in the thought with things to here is a little presentation and the player of the player.

      + What are the deview of the intersted be corded to and them all the world and the conteraction of the final self.

      + How to chologred and what I want to had the world

      + A come to and the tood to you don't feel like things that well

      + 

  + ---

  + " I'm them and to be speciated to be been about this like they to sort of community and the really for things and there is a sember that the sure and the world by [Many Worlds Game/version/5]({{< ref "Many Worlds Game/version/5" >}}) was sure a planning in the stranting

    + I want to feel learn that we construtions of the inter in the interent the way to be all in the world but the little with the wolds and the today.

      + I how my emall like the world is interacting and the learn you make a complex and contration and the tooth the manie int"

  + ---

    + " and out of with this to think about [[thesis]]

      + West happent this similar diness that was but of all some starting a like it about what also the sure what if the world about my them. I was to things to do something still how do what are the conteractive and them it was being again the particular thing that was a little wanter to the but a lot of strange the happen to community that was that it a self the down to be dessond down which a blocked and the thoug in the connections of something "
