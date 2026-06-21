Community:
  The community that I choose was the swimming subbreddit (r/swimming). I choose this community because there were many posts on this page from a variety of different users, from ex-Olympians to recreational swimmers.
  This community is a good fit for a classification task since there are posts giving advice, asking for advice, stating facts, and more.

Labels:
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

Data collection plan:
  I will collect examples from r/swimming. I will try to collect around 50 per label so that the 200 examples will be about evenly split between the four labels. If a label is underrepresented after 200 examples,
  I will go back and try to find more examples from that label to maintain balance.

Label distribution:
    Receiving_Advice    87
    Update              49
    Advice              36
    Recommendations     28
  
Difficult-to-Label Examples:
      - "I broke the 100m free WR??!": Update — it's a satirical post sharing an image of a time, but the intent is sharing a data artifact, not asking for help. Flagged as potentially satirical.
      - "4 months into swimming: is 2:43/100m decent?": Update — the post shares personal performance data (image from smartwatch) and asks "is this good?" The primary content is a data share and the question is                   secondary. Compare with posts like "I haven't swam in 8 years..." which are purely seeking technique help.
      - "Swam my first kilometer yesterday!": Advice — primarily a milestone share with some embedded questions at the end, but the post's purpose is sharing experience.

Fine-Tuning Approach:
  Base Model - distilbert-base-uncased
  Training Setup - 70% of the 200 examples where used as part of the training dataset. Precision, Recall, Accuracy, and F1 Score were reported.
  Hyperparamter Decision - the number of epochs was increased from 3 to 5 and the learning rate was decreased from 2e-5 to 1e-5. This was done so that the model could learn the data more and in a more stable way.

Evaluation Report:
  Overall Accuracy: For the Baseline model it was 0.667. For the Fine-Tuned model it was 0.433.

  Per-class metrics (baseline):
                  precision    recall  f1-score   support

          Advice       0.50      0.33      0.40         6
Receiving_Advice       0.62      1.00      0.76        13
 Recommendations       1.00      0.50      0.67         4
          Update       1.00      0.43      0.60         7

        accuracy                           0.67        30
       macro avg       0.78      0.57      0.61        30
    weighted avg       0.73      0.67      0.64        30

  
  Per-class metrics (fine-tuned model):
                    precision    recall  f1-score   support
  
            Advice       0.00      0.00      0.00         6
  Receiving_Advice       0.43      1.00      0.60        13
   Recommendations       0.00      0.00      0.00         4
            Update       0.00      0.00      0.00         7
  
          accuracy                           0.43        30
         macro avg       0.11      0.25      0.15        30
      weighted avg       0.19      0.43      0.26        30

  Confusion Matrix:
                 Advice   Receiving_Advice   Recommendations   Update
         Advice    0               6                0            0
Receiving_Advice   0              13                0            0
Recommendations    0               4                0            0
          Update   0               7                0            0

  Wrong Predictions:
  Wrong predictions: 17 / 30
      Example 1:
      Text:      Quick intro so you know why I'm writing this: I'm JosÃ©. I swam distance freestyle for Portugal for about ten years, the 800 and 1500, with a stop at the Tokyo 2020 Olympics. Somewhere along the way, ...
      True:      Advice
      Predicted: Receiving_Advice  (confidence: 0.29)
      Reasoning: The post starts with a narrative about the user so the model may have read this and decided that it was in the Receiving_Advice category. I tried to make the examples I gathered evenly distributed
      among the four labels, but Receving_Advice did end up having the most posts. Due to this, the model most likely learned to predict this class the best, leading the model to treat this label as a "catch-all".
      
      Example 2:
      Text:      Curious what's worked for people here because my shoulders are starting to feel permanently annoyed. Started swimming consistently again and forgot how quickly upper back/shoulder tightness sneaks up....
      True:      Recommendations
      Predicted: Receiving_Advice  (confidence: 0.29)
      Reasoning: The destinction between the Recommendations and Receiving_Advice label is that the former is for adivce on non-technique related things while the latter is for technique related adivce. The model did not
      learn this distinction, most likely due to limited examples, and mistook this post to be Receiving_Advice.
      
      Example 3:
      Text:      I'm in month 3 of swimming and I'm addicted. I've tried two different methods while practicing front crawl. Method A: Continuing to breathe out all the way got me gasping for air in only 10-15 meters....
      True:      Advice
      Predicted: Receiving_Advice  (confidence: 0.32)
      Reasoning: The model learned Receiving_Advice to be a "catch-all" bucket and always chooses to label posts with this label. To change this overall, I need to include more examples from other labels and make sure that
      the model fully reads prompts before deciding which label to categorize them as.

  Sample Classification:
    Example 1:
    Text:      I have been playing around with this, sometimes I look down at the bottom and sometimes I look ahead and sometimes I just wander with my eyes. What do folks in this community suggest? I have noticed t...
    True:      Receiving_Advice
    Predicted: Receiving_Advice  (confidence: 0.30)
    Reasoning: The prediction is reasonable as the post asks for suggestions about head/eye movement while swimming which is related to technique.
    
    Example 2:
    Text:      Hii! I'm a swimmer from a small club and we did a long distance gala. We did as many lengths of a 25m pool as we could for an hour. I got 102, so roughly 2.5k. Im 13. Is this any good? [image of certi...
    True:      Receiving_Advice
    Predicted: Receiving_Advice  (confidence: 0.31)
    Reasoning: The prediction is reasonable as the post asks for suggestions about time standards which is related to overall swimming ability.
    
    Example 3:
    Text:      So it's coming into winter here in Australia and my local pool is outdoors. I currently swim 2 x a week long swims (90mins 5km) and then 2 x a week shorter swims (just 1km 20 mins after my runs as a c...
    True:      Update
    Predicted: Receiving_Advice  (confidence: 0.31)
    
    Example 4:
    Text:      I've been swimming regularly for about 8 months. My main issue is endurance. After 50 meters of freestyle, I usually need to stop for several seconds to catch my breath. My 100m freestyle time is arou...
    True:      Advice
    Predicted: Receiving_Advice  (confidence: 0.31)
    
    Example 5:
    Text:      I saw this post last month about someone who started swimming at 33 and it changed their life for the better, especially their mental health. As a swim teacher, I found this really inspiring. I'm real...
    True:      Update
    Predicted: Receiving_Advice  (confidence: 0.30)

Reflection:
  The model severely overfit to the Receiving_Advice label, classifying every post to be part of this. The model was intended to capture distinctions between each of the four labels and understand what each label means.
  However, likley due to a slight imbalance in data, the model understood Receiving_Advice to be a catch-all bucket and choose this label every time. The label distribution was 87 Receiving_Advice, 49 Update, 36 Advice,
  and 28 Recommendation.

Spec Reflection:
  The spec helped me tracked each step of the process and understand what each section and cell of the notebook would be used for. Additionally, the planning section at the beginning of the spec allowed me to brainstorm
  ideas and understand the project/model so that I could choose a community that fit within the project's scope. One way that my implementation diverged from the spec was that I changed the number of epochs and the
  learning rate of the model and re-ran section 3. I did this because when I ran section 3 with 3 epochs and a learning rate of 2e-5, the accuracy was very low. I decided that adding more epochs and lowering the learning
  rate could improve accuracy and it did make a difference in the output.

AI Usage:
  I used AI, Claude, to assist me in labelling half of the examples. I gave it my labels and my edge-cases and asked it to follow those guidelines

  I asked Claude to help me understand why my model was consistently labelling every posts as Receiving_Advice as well as other pattern in my wrongful predictions. I gave it my wrongfully predicted output for context.
  The response that I got stated that this was most likely not a labelling problem, but rather the result of a small and imbalanced dataset.

  I was receiving errors as I tried to run the notebook so I asked Gemini to fix the errors. It added import statements that I checked and made sure worked. I also asked Gemini to include a F1 score indicator directly
  in the code alongside the accuracy measure so that I could look at both metrics to measure the accuracy of the model.
    
