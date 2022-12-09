# Legal Simplification Using GPT-3
## Contributors:
- Andrew Lona

## Project Prompt (2)
Option 2: Implement an interesting application on top of a Large Language Model, such as GPT-3. These models can write stories, play games, write programs, generate images (Stable Diffusion), and ... do lots of other things, which we're only discovering now. What happens when you hook these things together?

A good application will go beyond the basic things that you can do with Large Language Models. For example, just making an API call to GPT-3 is not sufficient. Here are some ways to get a good grade (you don't have to do all of them at once, and others may be possible):

- You have found a creative way to chain together Large Language Models with each other or other parts of the software stack.
- Your application addresses a real / interesting user need.
- You have found a non-obvious capability of Large Language Models.
- Your application provides a good user experience.

## Goal for this project
The goal is to create a law simplification pipeline/application for CA Legislature bills.
## Literature Review, detailing the need/importance of legalese simplification, along with background research into the topic which should potentially speed up progress.
    - *Poor writing, not specialized concepts, drives processing difficulty in legal language* (Martinez, et al., 2022)
        - Details how legalese comprehension difficulty is not just noticeable, but directly tied to poor writing practices. Provides framework for testing and goals for scaling readability.
    - *Plain English Summarization of Contracts* (Manor and Li, 2019)
        - An earlier attempt at legalese simplification, albeit with a simpler model and more statistically rigid readability scoring criteria. Also says "this is a very challenging task" (p. 2)

### Python Code Integration Process. Both in code and as a brief writeup of process + results.
    - Regarding Pipeline/process stitching, I am hoping to combine web scraping, reading difficulty classification, and comprehension level translation into a seamless process powered by GPT-3.
    - If there is more time available, a GUI for this application will be made (perhaps using GPT-3 to code the UI?), as well as a fine-tuned GPT-3 model to improve efficiency.
        - Although so far I haven't found a big need for fine-tuning GPT-3 yet, apparently others on Piazza are having worse performance with their fine-tuned models, so I decided for my efforts to be on testing and further literature research.
    - As such. the pipeline will follow this process in the code below...

    1. The user is asked to input a quote from an AB or SB bill they would like simplified and what level they would like it simplified to.
    2. The quote is then used to webscrape the entire bill text of the focused bill and location of said quote within the bill. will either be fed through GPT-3, an alternative model, a series of statistical formulas (simple model), or a combination to determine the 4 comprehensio
    3. This then scores for the text
        - word choice, word-frequency, and passive voice (embedded text and non-standard capitalization are unfortunately not finished but will continue to be worked on).
    4. These 3 scores are then compared to reference scores which provide levels of difficulty based off the Martinez et al. paper.
    5. GPT-3 is then fed this info along with the text, and is asked to simplify the text to the level given.
    6. GPT-3 then asked to do one or all of three things during this process and are tweakable as parameters.
        - If the difficulty of the text is higher than the difficulty of the example corpus, then GPT-3 will simplify before applying any theming. This is tweaked with corpus resizing of the sample.
        - If the simpified text is determined as too difficult still and can continue to be simplified, GPT-3 will be asked to continue the above process until the bill is understood. This is tweaked with pass size.
        - If the user provides GPT-3 with a theming prompt, then the simplified text will have a theme applied (either based on Social Media, Films, or Academic writing). This can be omitted but is left in as part of the UI for ease of use.
    7. After the process is finished, the simplified version of the bill is outputted to the user along with any additional information scraped to provide context.

## Brief analysis of results
    - 3 samples will be generated using this process and then presented to a paralegal for verification of accuracy (nothing too crazy, I don't want to take up their time)
    - Extra: if given enough time, these samples will be incorporated into a short quiz/survey (with random variations of the original and simplified texts at different steps) and sent out. Results of the survey will be compared to the results from the Martinez, et al. paper.

## What would success be at the end of this pipeline?
    - On a very simple-level, success would be both a simple interface with realistic outputs that do improve reader comprehension of Legalese
    - What this looks like is a usable translator where the user only has to interact with it on a basic level and
    - The simplified law snippets do indeed prove reader comprehension has increased (aka questions of simplified text tend to have more correct answers)
    - Because the purpose of this project is to deliver an easier to interpret message to users, that includes an easy to use GUI.
___

## Version Info

Python 3.9.14

Libraries Used:
openai
bs4
requests
random
PySimpleGUI
threading
re
nltk

System Version: macOS 12.6
      Kernel Version: Darwin 21.6.0
 Model Name: MacBook Pro
      Model Identifier: MacBookPro18,4
      Chip: Apple M1 Max
      Total Number of Cores: 10 (8 performance and 2 efficiency)
      Memory: 32 GB
