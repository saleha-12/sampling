# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Saleha Ejaz Qureshi

Analysis of Sampling in the Model
The model simulates a scenario where infections occur at different event types (weddings and brunches) and then undergo a biased contact tracing process. The sampling happens at multiple stages:

1. Initial Infection Sampling
•	Function Involved: np.random.choice(ppl.index, size=int(len(ppl) * ATTACK_RATE), replace=False)
•	Sample Size: 10% of the 1000 attendees (i.e., 100 people) are randomly selected to be infected.
•	Sampling Frame: All 1000 people attending weddings and brunches.
•	Underlying Distribution: Uniform random sampling (each person has an equal probability of being selected).

2. Primary Contact Tracing Sampling
•	Function Involved: np.random.rand(sum(ppl['infected'])) < TRACE_SUCCESS
•	Sample Size: 20% of the infected individuals (approx. 20 individuals if 100 are infected).
•	Sampling Frame: The subset of infected individuals.
•	Underlying Distribution: The selection is uniform random sampling.

3. Secondary Contact Tracing Sampling
•	Function Involved: event_trace_counts[event_trace_counts >= SECONDARY_TRACE_THRESHOLD].index.
•	Sample Size: Varies based on the number of events that meet the secondary tracing threshold.
•	Sampling Frame: Events with at least two traced infections.
•	Underlying Distribution: The selection is conditional based on primary tracing results.
This sampling method reflects the biased nature of real-world contact tracing, where structured events (weddings) are easier to trace than casual ones (brunches).

Relationship to the Blog Post
The blog post explains that contact tracing may lead to biased samples due to the ease of tracing in certain settings (e.g., weddings) compared to others (e.g., brunches). The model demonstrates this by showing how secondary contact tracing (when multiple cases are traced to the same event) can lead to an overestimation of cases from easily traceable events (weddings) and an underestimation from less traceable events (brunches).

Effect of Reducing Repetitions to 100
•	Modification: I have changed the range(1000) to range(100).
•	Observations: Running the script multiple times with 100 repetitions showed significant variation in peak locations and proportions, making the results less stable.

Making the Code Reproducible
To make the code reproducible, I’ve set a random seed, by adding this line at the beginning of the function:
np.random.seed(42)  
Effect:
•	Running the script multiple times has now yielded the exact same histograms every time.
•	The output doesn't match Whitby's blog post exactly but remained stable across runs.


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 16/02/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
