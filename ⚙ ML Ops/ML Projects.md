Lecture 5 : ML Projects

### Lifecycle

All the activities in an ML project. Not a linear step but an iterative project.

	1. Planning & project setup
	2. Data collection & labeling
		- Too hard to get data
		- Labeling process
	3. Training & Debugging
		- Implement baseline (open libraries)
		- Find SOTA model
		- Improve model
		- Collect more data
		- Task may be too hard & Requirements trade off with each other
	4. Deploying & testing
		- Performance in the real world…
		- Data mismatch between training data & deployment
		- Collect more data
		- Faster or more accurate?
	

### Prioritizing projects

	- Find high impact with feasibility (low cost..) 

	• The economics of AI
	  1. Prediction is central for decision making.
	  - AI reduces cost of prediction, even in problems where it was too expensive before. 
	  - Find cheap prediction which have a huge business impact.

	  2. Software 2.0 = Humans specify goals with datasets, and algorithm searches and optimizes the program. 
	  - Works better, more general, computational advantages (HW, SW)
	  - Hand-designed heuristics?
    - Complicated rule-based software can be learned to be automated instead of programming them.
	
	  3. Usecases
	  - Reducing costs (for predictions, automation)
	  - Generating customer insights (Reduce costumer churns)

	• 3 main Cost Drivers of ML projects
		1. Data availability
			- How hard is it to collect data, label data?
			- How much is needed?
			- How stable is the data? (Real world behavior changes)
			- Data security requirements
		2. Accuracy requirements
			- How costly are wrong predictions? (Recommendation system vs. Automated Drive)
			- Ethical issues (fairness)
			- Required Accuracy ~ Project Cost (High quality labels & Amount of data)
		3. Problem difficulty
			- Well-defined problem
			- Compute requirements (research vs real-time mobile operation)
			
	• What's still hard with ML
		- Understanding humor / sarcasm
		- In-hand robotic manipulation (HW)
		- Generalize to new scenarios
		- Unsupervised learning / Reinforcement learning (only limited domains where tons of data and computation are available)
    
		- What types of problems are hard?  
    
    		- Output is complex : High dimension (Video prediction, 3D), Ambiguous, open output (Dialog, Open-ended recommendation)
			- Reliability required (High precision, robustness)
			- Generalization is required : Out of distribution, Reasoning/Planning/Causality (Edge cases, Control, Small data)


### Archetypes

Build automated data flywheels. 

	• Software 2.0 (Make it fast, automate)
	• Human-in-the-Loop (Generate & reviewed by human)
	• Autonomous systems (Fully automate)

  - ML product design guidelines  
	  Good product design may…  
	  Reduce need for high accuracy (Face tagging, Grammar correction, Recommender system)  
	  Just provide users with better experiences by suggesting multiple choices.  
	
  - How can the model learn from the users?  
	  Explicit or implicit feedback  
	  Sub-driven data (face ID)
		

### Metrics

	• Choosing a metric
	- Error may differ in various metrics
	- ML systems work best when optimizing a single number.
	- Need to pick a formula to combine metrics
	
	• Combining metrics
	- Simple average / Weighted average
	- Choose metrics & Thresholds
		- Through domain judgement 
		- Least sensitive to model choice (Not vary a lot)
		- Closest to desirable values
	- More complex & domain specific metrics (ex. mean Average Precision over classes)


### Baselines

Good baselines help you invest effort in the right way.

	- Scripted baselines (OpenCV, rule-based)
	- Simple ML baselines (bag-of-words, linear regression, averaging)
	- Human baselines (Specialized domains : more expertized labelers)
