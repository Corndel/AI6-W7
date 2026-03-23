# Coach Playbook
## Workshop 7: Production Grade Classification
### Corndel AI6 Level 6 ML Engineer Apprenticeship

---

## Pedagogy intent and programme positioning

This workshop sits at the end of Unit 7, after learners have covered evaluation metrics (7.2), advanced modelling concepts (7.3), and the deployment decision framework (7.4). It is the practical synthesis of all three.

The central question is not "can you build a classifier" : learners have done that. The question is "can you make and defend the decisions that turn a classifier into something deployable." That means choosing the right metric, handling class imbalance, setting a threshold you can justify, and removing features that should not be in the model even if they improve performance.

The IBM HR attrition dataset is intentionally imperfect. The model will not be impressive. That is the point. A ROC AUC of around 0.63 is weak signal, and learners need to sit with that and decide whether it is good enough for the use case and why. A clean model they cannot explain is worse than a modest model they understand.

The four uncomment tasks are deliberate retrieval practice. Learners should know train/test splits and threshold application from earlier units. Struggling here is information: if they cannot do it, earlier material needs revisiting.

The four collapsible Q&A blocks are for learners who want to go deeper. Do not read them aloud. Let learners open them if they want to. The DPIA one in particular is worth flagging at the start of Section 6 if the group seems unaware.

WandB is the production-grade moment. By the end of the session every learner has a real experiment tracking dashboard showing four deliberate decisions and their effects. That is portfolio evidence and a genuine professional skill.

---

## Session plan and timings

| Time | Section | What should be happening | Watch for |
|:--|:--|:--|:--|
| 09:00 | Setup | Codespaces open, WandB login | Anyone without API key: share yours temporarily, they create their own after |
| 09:20 | Section 1 | Data loading, class distribution | Learners should notice the imbalance before you point it out |
| 09:40 | Section 2 | Naive model, accuracy trap | The penny-drop moment at the confusion matrix. Give it time. Do not rush to the fix. |
| 10:10 | Section 3 | Imbalance fix, scale_pos_weight | The uncomment task here surfaces whether learners understood the concept |
| 10:40 | Break | | |
| 10:50 | Section 4 | Threshold table, choose and justify | Most important conversation of the morning. Push back on anyone who picks a threshold without a reason. |
| 12:00 | Lunch | | |
| 13:00 | Section 5 | SHAP, feature importance | Ask: which features surprised you? Which ones worry you? |
| 13:45 | Section 6 | Feature selection, DPIA question | Flag the DPIA collapsible. Ask who has heard of a DPIA before. The updated table with Possibly column usually generates good discussion. |
| 14:30 | Section 7 | WandB dashboard review | Ask each learner to summarise their four runs in one sentence each. |
| 15:00 | Break | | |
| 15:10 | Section 8 | Wrap-up questions | These are conversation starters, not written tasks. Aim for the whole group to hear different answers to question 3 (feature removal justification). |
| 15:40 | Close | | Remind learners their WandB project is permanent evidence. Encourage them to add it to their learning journal. |
| 15:40 | Section 9 | WandB model registration | Check everyone has a model saved to disk before moving to FastAPI |
| 16:00 | Section 10 | FastAPI wrapper | They write app.py and see the structure. Do not spend time on Kubernetes theory unless asked. |
| 16:25 | Section 11 | Model card | The most reflective part of the day. Give it time. |
| 16:45 | Close | | Model card + WandB project are portfolio evidence. Learning journal. |

---

## Troubleshooting

**WandB login fails**
The fallback is already in the login cell as a comment. Ask the learner to comment out the `wandb.login()` line and uncomment the `wandb.init(mode='disabled')` line. Everything runs normally, they just will not have a dashboard at the end. They can create an account later and replay the session.

**utils.py not found**
The notebook raises a clear error naming the expected file location. The cause is almost always that the learner opened the notebook directly rather than cloning the repo. Ask them to close the tab, go to the repo, and open the Codespace from there. The file should be present automatically.

**ibm_attrition.csv not found**
Same cause as above. The CSV must be in the same directory as the notebook. If the Codespace is open correctly, it will be there.

**Uncomment task produces an error**
This is expected for the wrong options. If a learner gets an error, ask them which line they uncommented and why. If they uncommented a correct-looking wrong option, use it as a teaching moment about why that specific approach fails.

**SHAP takes too long**
It should not: 294 rows takes under a second. If it is slow, the Codespace may be under-resourced. Ask the learner to restart the kernel and run from the top.

**Learner picks threshold 0.5 and cannot justify it**
The default is not a justification. Ask: what does a false negative mean for an employee in this system? What does a false alarm mean? Which would you rather explain to the HR director? Push until they give a human answer, not a metric answer.

**Learner wants to keep Age in the model**
Do not override them. Ask them to document the reasoning in the code comment and make sure they can answer question 3 in the wrap-up. The point is the reasoning, not the specific feature list.

**joblib or fastapi not installed**
The setup cell installs everything. If a learner skipped the setup cell, ask them to run it first. If it fails, the Codespace may not have network access: `pip install joblib fastapi uvicorn pydantic --break-system-packages`.

**app.py column mismatch error**
The app.py is generated using the FEATURES_TO_REMOVE list from the notebook. If a learner changed that list and then ran the app.py cell without updating, the columns will not match the saved model. Ask them to rerun the app.py writer cell.

**Model card feels overwhelming**
Tell learners to fill in the performance table first using WandB numbers, then the feature removal section using what they already decided. The rest follows naturally. They do not need to write perfect prose: bullet points in the limitation and risk sections are fine.

---

## KSB coverage
Primary KSBs are those most directly and substantially evidenced by work produced in this workshop. Secondary KSBs are reinforced here but were introduced earlier or will be revisited in later units.

### Primary KSBs
**These require the most focus during delivery and assessment.**

| KSB | Description | Where evidenced |
|:--|:--|:--|
| **K7** | Performance metric selection in business context | Accuracy trap, F1 vs recall, threshold justification (Sections 2-4) |
| **K19** | Problem-solving via test data analysis including edge-case data | Stress-testing with real test profiles and counterfactual reasoning (Section 12) |
| **S11** | Regulatory, legal, ethical and governance issues at each stage | Feature selection, DPIA, Equality Act, throughout Sections 5-14 |
| **S14** | Analyse test data, interpret results, evaluate solution suitability | Confusion matrix, ROC AUC, threshold table, stress-test profiles (Sections 2-4, 12) |
| **S20** | Minimise algorithmic bias | SHAP analysis, feature removal, documented in model card (Sections 5-6, 11) |
| **B4** | Acts with integrity, legal and ethical requirements | Threshold justification, feature removal, accountability questions throughout |
| **B5** | Operates in technical complexity and uncertainty | Borderline threshold decision, stress-test edge cases, ROC AUC calibration |

### Secondary KSBs
Reinforcement of ideas introduced in earlier units or revisited in later ones.

| KSB | Description | Where evidenced |
|:--|:--|:--|
| K5 | ML methods and experiment tracking tools | XGBoost throughout; WandB logging and model registration (Sections 3-9) |
| K29 | Own role in relation to organisational governance, legal and ethical practice | Handoff discussion, accountability wrap-up, model card (Sections 10b, 13, 14) |
| S5 | Create and deploy models | FastAPI wrapper, joblib model saving (Sections 9-10) |
| S6 | Document model lifecycle assets | WandB run history, model card, app.py (Sections 9, 11) |
| S28 | Produce and maintain technical documentation for the data product | Model card completed with real results (Section 11) |
| S29 | Create reports and presentations for stakeholder approval and handover | Three-slide executive summary, handoff discussion (Sections 13, 14) |
