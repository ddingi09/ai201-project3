Create planning.md in your repo root. Design the section structure yourself. At minimum, your document must substantively address these six questions:

Community: What community did you choose and why? Why is this community a good fit for a classification task — what makes the discourse varied enough to be interesting?

The community that I choose was the swimming subbreddit (r/swimming). I choose this community because there were many posts on this page from a variety of different users, from ex-Olympians to recreational swimmers.
This community is a good fit for a classification task since there are posts giving advice, asking for advice, stating facts, and more.

Labels: What are your 2–4 labels? Define each in a complete sentence. Include 2 example posts per label.

  Advice - the post give a suggestion to the channel, it can be based off of personal experience or fact, evidence is not necessary. The advice can be general or targetted to a specific group.
    Examples:
         - You're not fading in the back half because you're unfit. You're going out too fast. Quick intro so you know why I'm writing this: I swam distance freestyle internationally. 
         800/1500 free, raced for Portugal at the Tokyo Olympics, held my country's record in both and I coach adult swimmers now.
         - I forgot swimming is the best exercise. I was a star swimmer from 6-18. Left high school with 7 school records, competed at nationals junior and senior year etc.
         
  Receiving_Advice - the post asks for help on how to improve technique or overall swimming ability. Can included narration to give context for the question or just be a single sentence with a question mark.
    Examples:
         - Of course I know the general motion, you can tell that just from seeing others swim, but I feel like I'd get in the water for the first time just to find out I basically cant swim anymore.
           I don't know if muscle memory will save me orrr...Has anyone been in a similar situation?
         - Does anyone have any ideas for helping a kid understand how to move his body faster?
  
  Recommendations - the post asks for help on anything other than actual technique. Can be problems while swimming or any general questions.
    Examples:
         - how to prevent water from going in nose without a plug? nothing has really worked
         - Best stretches to improve shoulder mobility? My dolphin kicking is horrible due to poor flexibility. 
  
  Update - the post gives a headline about recent news, events, or personal happenings. evidence, in the form of a link, citation, or paraphrase, to inform the channel about the result of a recent competition or any other swimming related news.
    Examples:
         - Kate Douglass breaks Sarah Sjostrom's world record in 50 free https://swimswam.com/kate-douglass-breaks-sarah-sjostroms-world-record-with-23-59-50-free/
         - I came across this article in Popular Mechanics the other day, Water Alters Your Consciousness, Research Suggests—And Can Induce a Trance-Like State https://archive.ph/i3Hu3

Hard edge cases: What type of post will be genuinely ambiguous between two labels? How will you handle it when you encounter it during annotation?

  Posts that state a link but then also ask for advice could be hard to classify between Update and Recieving_Advice. Similarily, there are many posts that give a satirical update with evidence that is false.
  When I encounter these types of posts, I will decide which category it goes in based on the end goal of the post. For example, a post that gives evidence but still asks for advice would go in the Recieving_Advice
  classification because the user is still asking for help. A post that gives incorrect evidence would be classified as Update but I will include a disclaimer saying that not all information may be correct in the final
  output of the LLM.

  Examples:
      - "I broke the 100m free WR??!": Update — it's a satirical post sharing an image of a time, but the intent is sharing a data artifact, not asking for help. Flagged as potentially satirical.
      - "4 months into swimming: is 2:43/100m decent?": Update — the post shares personal performance data (image from smartwatch) and asks "is this good?" The primary content is a data share and the question is                   secondary. Compare with posts like "I haven't swam in 8 years..." which are purely seeking technique help.
      - "Swam my first kilometer yesterday!": Advice — primarily a milestone share with some embedded questions at the end, but the post's purpose is sharing experience.

Data collection plan: Where will you collect examples? How many per label? What will you do if a label is underrepresented after 200 examples?

  I will collect examples from r/swimming. I will try to collect around 50 per label so that the 200 examples will be about evenly split between the four labels. If a label is underrepresented after 200 examples,
  I will go back and try to find more examples from that label to maintain balance.

Evaluation metrics: Which metrics will you use to evaluate your model and why are those the right ones for this specific task? (Accuracy alone is not enough — explain what else you need and why.)

  I will use precision and recal to evaluate my model. These are the right metrics as precision measures the reliability of classifications and recall measures the model's ability to identify the correct
  classifications. Put together, these two metrics will allow me to understand the model's overall classification ability. Since increasing precision usually lowers recall and vice versa, I will calculate the F1-score
  to balance these two metrics and get a final result.

Definition of success: What performance would make this classifier genuinely useful? What would you accept as "good enough" for deployment in a real community tool?

  An F1-score above 0.80 is usually considered to be good. Since this model is trained on 200 examples, I will say that an F1-score above 0.70 is "good enough".

Add an AI Tool Plan section to your planning.md. This project's workflow is different from implementation projects — there's no code to generate, so your plan should cover the three places where AI tools actually help here:

AI Tool Plan:

  Label stress-testing: Give the AI your label definitions and edge case description, and ask it to generate 5–10 posts that sit at the boundary between two labels.
  If it produces posts you can't classify cleanly, your definitions need tightening — do that now, before you annotate 200 examples.

  Advice vs Recieving_Advice
  1. Recieving_Advice - I used to struggle with bilateral breathing and eventually just forced myself to only breathe to my weak side for an entire month — uncomfortable but it worked for me.
  Do you think that's still the best approach or has coaching moved on from that?
  
  Update vs Receiving_Advice
  2. Receiving_Advice: Saw this piece saying cold-water immersion before a race can prime your nervous system for better starts: https://swimmingscience.net/cold-water-priming — 
  has anyone actually tried this? My reaction times at the block are embarrassingly slow and I'm desperate.
  
  Advice vs Recommendations
  3. Advice: Honestly the best thing I ever did for my shoulder was ditch paddles entirely for three months. No product recommendation, just rest and scapular activation drills. 
  If you're in pain, stop adding load before you fix the pattern.
  
  Update vs Advice
  4. Update: Leon Marchand just went sub-4:00 in the 400 IM in training — unverified clip going around on Twitter. Whether it's real or not, watching his underwaters will teach you more about dolphin kick timing than any drill set. Study the footage.
  
  Receiving_Advice vs Recommendations
  5. Recommendations: I keep getting water up my nose on flip turns no matter what I try — I've watched tutorials, tried exhaling through my nose, even bought a clip. Is this a technique problem or am I just built differently?
  
  Advice vs Update
  6. Update: There's a new USA Swimming study out on taper protocols for masters athletes — the short version is that older swimmers need longer tapers than the 10-day standard.
  I've been doing 3-week tapers for years and my meet results back this up completely.
  
  Receiving_Advice vs Recommendations
  7. Recieving_Advice: My 9-year-old keeps dropping his elbow on his catch. I've tried every cue I can think of — "reach over the barrel," fingertips down, even showed him video.
  At what point does this become a physical limitation vs a comprehension thing, and are there any drills or tools that actually work for kids this age?
  
  Update vs Advice
  8. Advice: Just read that SwimSwam did a breakdown of the top-10 200 fly splits from last year's World Championships and every single one of them had a faster third 50 than their second.
  If your race plan has you "holding on" through the back half you're already losing.

  Annotation assistance: Decide whether you'll use an LLM to pre-label a batch of examples before reviewing them yourself.
  If yes, note which tool you'll use and how you'll track which examples were pre-labeled (for disclosure in your AI usage section).
  
  I'll use an LLM, specifically Claude, to label half of my examples. These will be listed as the first 100 examples in the document.

  Failure analysis: Plan to give your list of wrong predictions to an AI tool and ask it to identify patterns before you write up your evaluation.
  Note what you'll look for and how you'll verify the patterns yourself.

  I'll look for whether the pattern shows that the wrongful predictions are for posts that are between two labels. I'll verify these patterns myself by going through the exampls that were wrongfully classified and checking
  if they are difficult for me to place in a single label.
