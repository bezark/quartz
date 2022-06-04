---
title: LogSeq P5 Page Word Cloud
tags:
categories:
date: 2022-05-29
lastMod: 2022-05-29
---
What I decided to go for though was simply getting a wordcloud into a p5 plugin from my [[Logseq]] page entries. Clicking the graph button creates a word cloud for all times I've linked to that page. That's really nice because in logseq, essentially anything can be a page, and I have a lot of pages for specific parts of my life:

  + [[journal]] entries

  + [[Dreams]] for my dream journals

  + emotional concepts like when I'm [[hard on myself]]

  + and all sorts of stuff!

<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe src="https://www.loom.com/embed/d02f59e72eac432c9813a115e6196818" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>



Here's the [GitHub Repo](https://github.com/bezark/p5-logseq-wordcloud)

## How I did it

  + I found this decent example for making a wordcloud in p5 with rita,js

  + [[p5 js]] [[Language analysis]] Examples

    + [Wordcloud](https://editor.p5js.org/fauthereea/sketches/aKByHsRr2)

```js
let params = {
    ignoreStopWords: true,
    ignoreCase: true,
    ignorePunctuation: true
  };
let counts = RiTa.concordance(lines.join(" "),
    params); 
let total = totalValues(counts);
```

    + The [[logseq]] api is fairly straightforward and allows you to create plugins that are essentially just iframes that can be opened and closed.

      + There's an index.js file with this stuff

        + 

```js
/**
 * User model
 */
function createModel () {
  return {
    openSketch () {
      // logseq.App.showMsg('hello, mind map')
      logseq.showMainUI()
    },
  }
}

function main () {
  logseq.provideStyle(`
    @import url("https://at.alicdn.com/t/font_2409735_lkeod9mm2ej.css");
  `)

  logseq.setMainUIInlineStyle({
    // position: 'fixed',
    // zIndex: 12,
  })

  logseq.App.registerUIItem('pagebar', {
    key: 'another-open-mind',
    template: `
     <a data-on-click="openSketch" title="open sketch">
       <i class="iconfont icon-icons-mind_map" style="font-size: 18px; line-height: 1em;"></i>
     </a>
    `,
  })

  // main ui
  // const root = document.querySelector('#app')
  const btnClose = document.createElement('button')
  const displaySketch = document.createElement('div')

  // events
  displaySketch.id = 'sketchey'


  // displaySketch.classList.add('mind-display', 'hidden')
  btnClose.textContent = 'CLOSE'
  btnClose.classList.add('close-btn')

  btnClose.addEventListener('click', () => {
    logseq.hideMainUI()
  }, false)

  document.addEventListener('keydown', function (e) {
    if (e.keyCode === 27) {
      logseq.hideMainUI()
      p.noLoop()
    }
  }, false)

  logseq.on('ui:visible:changed', async ({ visible }) => {
    if (!visible) {
      displaySketch.classList.add('hidden')
      displaySketch.innerHTML = ''
      return
    }

    let currentPage = await logseq.Editor.getCurrentPage()
    
    let backlinkedBlocks = await logseq.DB.datascriptQuery(`[:find (pull ?b [*])
    :where
    [?b :block/path-refs [:block/name "`+currentPage.name+`"]]
    [?page :block/original-name ?name]]
`)
    // console.log(backlinkedBlocks)
    let textHonk = []
    for (const blocky of backlinkedBlocks) {
      textHonk.push(blocky[0].content)
     
    }
    // const blocks = await logseq.Editor.getCurrentPageBlocksTree()
    initSketch(displaySketch, btnClose, textHonk)
  })

  // mount to root
  // root.append(displaySketch)
}

/**
 * @param el
 * @param btnClose
 * @param data
 */
function initSketch (el, btnClose, data) {



  if(!p){p = new p5(sketch, 'sketchey');}
  p.updateWordsToDraw(data)
  p.loop()

  // let mind = new MindElixir(options)
  // mind.init()

  const patchRightBottomBar = () => {
    // const barWrap = document.querySelector('toolbar.rb')
    // barWrap.appendChild(btnClose)
  }

  setTimeout(() => {
    patchRightBottomBar()
    // mind.initSide()
    // el.classList.remove('hidden')
  }, 16)
}

// bootstrap
logseq.ready(createModel(), main).catch(console.error)

```

      + And then a sketch.js with this stuff

    + Notably, p5 is in instance mode so it can attach nicely to the div that logseq makes.

  + The real tricky part was figuring out how to get logseq to query itself for all the blocks with the correct pages

    + The database is built in datomic/datascript and the syntax for that query was

```js
   let backlinkedBlocks = await logseq.DB.datascriptQuery(`[:find (pull ?b [*])
    :where
    [?b :block/path-refs [:block/name "`+currentPage.name+`"]]
    [?page :block/original-name ?name]]
`)
```

      + I don't realllly know how that worked, but it did!

  + There's still some cleaning up to do with it, but I'm already finding it a really interesting tool!

# Next Steps

  + https://t.co/vq3ii3p3My

  + [Nearley](https://nearley.js.org/)
