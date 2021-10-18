# TRUSTWORTHY ONLINE CONTROLLED EXPERIMENTS

**Part I Introduction😉**

- Intro
    - Term
        - Overall Evaluation Criterion (OEC): A quantitative measure of the experiment‘s objective. The OEC must be **measurable in the short term** (the duration of an experiment) yet believed to **causally drive long-term strategic** objectives, and **sensitive enough to show difference**.
        - Parameter: A **controllable** experimental variable that is thought to **influence** the OEC or other metrics of interest. Uni-variable with multiple values, or MVTs (Multivariate Tests)
        - Variant: A user experience being tested, typically by assigning values to parameters. In a simple A/B test, A and B are the two variants, usually called Control and Treatment
        - Randomization Unit: A pseudo-randomization (e.g., hashing) process is applied to units (e.g., users or pages) to map them to variants.
            - map units to variants in a **persistent** and **independent** manner
            - very common, and we highly recommend, to use **users** as a randomization unit when running controlled experiments for online audiences
            - Proper randomization is **critical**!
            
    - Why Experiment? Correlations, Causality, and Trustworthiness
        
        Benefits of online controlled experiments:
        - The best scientific way to establish **causality with high probability**.
        - Able to detect **small changes** that are harder to detect with other techniques, such as changes over time (**sensitivity**).
        - Able to detect **unexpected changes**. Often under-appreciated, but many experiments uncover surprising impacts on other metrics, be it performance degradation, increased crashes/errors, or cannibalizing clicks from other features.
        
    - Necessary Ingredients for Running Useful Controlled Experiments
        - There are experimental units (e.g., users) that can be assigned to different variants with **no interference** (or little interference)
        - There are enough experimental **units** (e.g., users). For controlled experiments to be useful, we recommend thousands of experimental units: the larger the number, the smaller the effects that can be detected.
        - Key metrics, ideally an **OEC,** are agreed upon and can be practically evaluated.
        - **Changes** are easy to make.
        
    
- Experiments according to the strategies/tactics
    
    "*Controlled experiments allow you to significantly reduce uncertainty by trying a MVP, getting data, and iterating, given the concept - **EVI** **(expected value of information)**!"*
    
    - Key Scenario 1: Business Strategy + Large User Units
        - Experiments help identify areas with high ROI - reach local optimum - **hill climbing**
        - Experiments help with optimizations on inconspicuous areas that could make a large difference or on backend algorithms and infrastructure
        - Experiments help with continuous iterations
    - Key Scenario 2: Product + Business Strategy + Need of a Pivot (radical changes)
        - Duration of experiments (primacy effects and change aversion)
        - The number of ideas tested - each experiment tests for one tactic as one component of the overall strategy
- Running and Analyzing Experiments
    - Setting up the Example
        
        Example → Evaluate the impact of simply adding a coupon code field ("fake door approach")
        
        Hypothesis → Adding a coupon field at the checkout page would degrade revenue
        
        OEC → Key metrics is **normalized** by the actual sample sizes - revenue-per-user 
        
        Redefine Hypothesis → Adding a coupon field at the checkout page would degrade **revenue-per-user for users who start the purchase process.**
        
    - Hypothesis Testing: Establishing Statistical Significance
        - "**Characterize** the metric" → understanding the baseline mean and standard error of the mean
        - "Assess **Statistical** **Significance**" → Compute **the p-value** for the difference between a pair of control and treatment samples
        - "Assess Statistical Significance" → Check whether **confidence interval (95% or higher)** **overlaps with zero** - for fairly large sample sizes it is usually centered around the observed delta between the Treatment and the Control with an extension of 1.96 standard errors on each side.
        - Statistical **Power**: the probability of **detecting** a meaningful difference between the variants when there really is one (statistically, **reject the null when there is a difference**) — Get more power when the **sample** **size** is larger; **80% - 90% power**
        - "Set the **Practical** **Significance** **Boundary**" → the magnitude of difference from a business perspective (ROI)
    - Designing the Experiment
        
        1. What is the **randomization unit**? 
        
        → "Users", or pages...
        2. What **population** of randomization units do we want to target? 
        
        → Users with particular characteristic (e.g. languages, geographic regions, platforms, and device types...)
        3. How large (**size**) does our experiment need to be? 
        
        → Direct impact the precision of the results - Sensitivity, Power 
        
        → Run larger experiments 
        
        - **HOW DO WE DECIDE EXPERIMENT SIZE?**
            - OEC: OEC with less variance needs smaller sample size to achieve the same sensitivity (e.g. purchase indicator v.s. revenue-per-user)
            - Practical Significance Level: bigger changes, easier to detect → smaller sample size needed
            - Statistical Significance Level (p-value threshold): lower/stricter threshold requires larger sample size
            - User Reaction: "Change Aversion", "Primacy/Novelty Effect"
            - Traffic Requirement: share traffic with other experiments, balance traffic requirement
        - **HOW LONGER WE RUN THE EXPERIMENT?**
            - More users: users trickle into experiments over time but often with sub-linear growth
            - Day-of-week Effect: capture weekly cycle; running for at least a min of one week
            - Seasonality: external validity
            - Primacy and Novelty Effects: Some experiments tend to have larger or smaller initial effect that takes time to stabilize
        
        Example:
        
        1. The randomization unit is a user.
        2. We will target all users and analyze those who visit the checkout page.
        3. To have 80% power to detect at least a 1% change in revenue-peruser, we will conduct a power analysis to determine size.
        4. This translates into running the experiment for a minimum of four days with a 34/33/33% (equal) split among Control/Treatment one/Treatment two. We will run the experiment for a full week to ensure that we understand the day-of-week effect, and potentially longer if we detect novelty or primacy effects
        
    - Running the Experiment and Getting Date
        
        Instrumentation: get logs data
        
        Infrastructure: platform and structure to run experiments
        
    - Interpreting the Results
        - Sanity Check: guardrail metrics/invariants → those metrics should not change between the Control and Treatment
        - Statistical Significance and Practical Significance
    - From Results to Decisions
        - Tradeoffs between different metrics, e..g engagement up but revenue down
        - Cost of Launching: if high—-make sure practical significance boundary is high enough to reflect that
            - Cost of fully build out the feature before launch
            - Cost of on-going engineering maintenance after launch
        - Cost of wrong decisions: when opportunity cost is high
        - Statistical Significance and Practical Significance
            
            1.Neither statistically nor practically significant → either iterate or abandon the idea
            
            2.Both statistically and practically significant → launch!
            
            3.Not practically significant but statistically significant → confident about magnitude but it might not be outweigh other factors as costs → may not worth launching 
            
            4.(Similar to 1) Neural → not enough power to draw a strong conclusion or make launch decision → run a **follow-up** test with more units to have greater statistical **power**
            
            [5](http://5.No).Not statistically significant but likely practically significant → **repeat** the test with more units to have greater statistical **power**
            
            6.Likely statistically and practically significant → **repeat** the test with more units to have greater **power**
            
            ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-05_at_4.29.44_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-05_at_4.29.44_PM.png)
            
- Twyman's Law and Experimentation Trustworthiness
    - Misinterpretation of the Statistical Results
        - Lack of Statistical Power : A common mistake is to assume that just because a metric is not statistically significant, there is no Treatment effect. It could very well be that the experiment is **underpowered** to detect the **effect size** we are seeing, that is, there are not enough users in the test.
            
            → define the practical significance threshold and ensure sufficient power to detect such/smaller magnitude
            
        - Misinterpreting p-values
            - The p-value is the probability of obtaining a result **equal to or more extreme** than what was observed, **assuming that the Null hypothesis is true.** The conditioning on the Null hypothesis is critical.
        - Multiple Hypothesis Tests: **False Discovery rate** is key concept to deal with this
        
    - Confidence Interval
        - Represents **how often** the confidence interval (computed from many studies) should **contain** the true Treatment effect.
        - For the Null hypothesis of no-difference commonly used in controlled experiments, a 95% confidence interval of the Treatment effect that **does not cross zero** implies that the p-value is < 0.05
        - Misunderstanding
            - look at the confidence intervals separately for the Control and Treatment, and assume that if they overlap, the Treatment effect is not statistically different. That is incorrect;The opposite, however, is true: if the 95% confidence intervals do not overlap, then the Treatment effect is statistically significant with p-value < 0.05.
            - Wrong belief that the presented 95% confidence interval has a 95% **chance** of containing the true Treatment effect; The 95% refers to **how often** the 95% confidence intervals **computed from many studies** would contain the true Treatment effect
            
        
    - Threats to Internal Validity
        - Correctness of the experimental results without attempting to generalize **to other populations or time periods**
        - Violations of SUTVA (stable unit treatment value assumption)
            
            SUTVA - **"the experiment units do not interfere with one another"**
            
            - Social Networks: a feature might spillover to a user's network
            - Skype:
            - Document Authoring Tools: co-authoring
            - Two-sided marketplaces (e.g. airbnb, eBay, lift—violate via other side)
            - Shared resources
        - **Survivorship Bias** (WWII - armors to bomber 😎)
            
            Analyzing users who have been active for some time (e.g., two months) introduces survivorship bias.
            
        - Selection Bias → Intention-to-Treat
            
            Analyzing only those who participate, results in **selection bias** and commonly overstates the Treatment effect. 
            
            **Intention-to-treat uses the initial assignment, whether it was executed or not**. The Treatment effect we are measuring is therefore based on **the offer, or intention to treat**, not whether it was actually applied.
            
        - Sample Ratio Mismatch (SRM)
            - If the ratio of users (or any randomization unit) between the variants is not close to the designed ratio, the experiment suffers from a Sample Ratio Mismatch (SRM).
            - Small imbalance can cause a reversal in Treatment effect: with large sample size, **an observed ratio** smaller than 0.99 or larger than 1.01 for a design that called for 1.0 more than likely indicates a serious issue. The experimentation system should generate a strong warning and hide any scorecards and reports, **if the p-value for the observed ratio is low/statistically significant** (e.g., below 0.001).
            - Cases likely to Cause SRM
                - Browser Redirects
                    - Causes SRM: performance differences (redirect latency for treatment users); Bots (Robots handle redirect differently); asymmetric and contamination (when user save or pass a redirect link to friends, no "authentication check" on a user to treatment page)
                    - Solution: Avoid redirects and prefer a server-side mechanism; (if not possible to avoid redirects) Redirect (the same 'Penalty') both Control and Treatment
                - Lossy Instrumentation - Click Tracking
                    
                    Click tracking is done using web beacons and not 100% clicks are recorded.
                    
                    - Causes SRM: When the web beacon is placed in a different area of the page, timing differences will skew the instrumentation.
                - Residual or Carryover Effects
                    
                    **Residual Effect** - It's common for new experiments to cause some unexpected issue and be aborted or kept running for a quick bug fix; after bug fixed, the experiment continues, but some users were already impacted. **Residual information in browser cookies** can also impact experiments
                    
                    **Carryover Effect** - In the opposite case, where an experiment is extremely beneficial, when it's stopped and restarted, there's a significant carryover effect. 
                    
                    - Run A/A test and proactively re-randomize users, recognizing that in some cases the re-randomization breaks the user consistency, as some users bounce from one variant to another.
                - Bad Hash Function for Randomization
                    
                    Some hash functions are sufficed for single-layer randomization but not for multiple concurrent experiments.
                    
                - Triggering Impacted by Treatment
                    
                    When triggering a segment of users into experiments are based on attributes that are changing over time, you must ensure that **no attributes used for triggering could be impacted by the Treatment.**
                    
                - Time-of-Day Effects
                    
                    Received email during work hours vs. after —> diff open rate 
                    
                    Open times clustered around diff time periods
                    
                - Data Pipeline Impacted by Treatment
                    
                    Bot filtering + clicks-per-users as user engagement → some of the most heavily engaged users were classified as bots and removed from analysis 
                    
                
    - Threats to External Validity
        
        The results of a controlled experiment can be generalized along axes such as different **populations** (e.g., other countries, other websites) and over **time** (e.g., will the 2% revenue increase continue for a long time or diminish?)
        
        - Generalization across populations - usually questionable, but can be tested by rerunning the experiment  in a different set of population (e.g. other countries, other websites)
        - Generalization over time - harder to assess the long-term effect
            - 2 Keys Threats to "Generalization over time"/"External Validity over Time"
                - **Primacy Effects**: users may need time to adopt as they are primed in the old feature
                - **Novelty Effects**: attractive at first but may not continue to use if users don't find it useful later → **treatment effect quickly diminish**
                - Detecting Primacy/Novelty Effect: **plot usage over time**
                    - Assumption: Treatment effects is **constant** over time
                    - Some need to run longer to determine when the Treatment effect stabilizes
                    - Option B - cohort analysis: take the users who appeared in the first day or two (as opposed to all users over time) and plot the treatment effect for them over time
            
    - Segment Differences
        
        What are good segments?
        
        - Market or country
        - Device or platform
        - Time of day and day of week
        - User Type: new or existing user
        - User account characteristics: single or shared account
        
        Segmented views are commonly used in two ways:
        
        1. Segmented view of a metric, independent of any experiment.
        
        When segmented by operating systems, the diff of CTRs caused by different click tracking methods or potential bugs.
        2. Segmented view of the Treatment effect for a metric, in the context of an experiment, referred to in Statistics as *heterogeneous* Treatment effects, indicating that **the Treatment effect is not homogenous or uniform across different segments →** Identifying interesting segments, or searching for interactions, can be done using machine learning and statistical techniques, such as Decision Trees and Random Forests
        
        - Analysis by segments impacted by Treatment can Misleading - when users move from one segment to another, interpreting metric movement at segment level can be misleading. Segments should be determined before experiment
    - Simpson's Paradox
        
        If an experiment goes through **ramp-up** that is, two or more periods with different percentages assigned to the variants, combining the results can result in directionally incorrect estimates of the Treatment effects, that is, Treatment may be better than Control in the first phase and in the second phase, but worse overall when the two periods are combined.
        
        Some cases where Simpson's Paradox may arise:
        
        - Users are sampled
        - An experiment runs on a website that is implemented in multiple countries
        - An experiment is run at 50/50% for Control/Treatment, but an advocate for the most valuable customers (say top 1% in spending) is concerned and convinces the business that this customer segment be kept stable and only 1% participate in the experiment. It is possible that the experiment will be positive overall, yet it will be worse for both the most valuable customers and for “ less-valuable” customers.
        
        **Observational data alone cannot help resolve this paradox, the causal model will determine which data to use** (the aggregation or the subpopulation)
        
        **"Sure-Thing Principle"** - if an action increases the probability of an event E in each subpopulation, it must also increase the probability of E in the population as a whole.
        
    - Encourage Healthy Skepticism
        
        anomalies, question results, invoke Twyman's Law when results are too good 
        
- Experimentation Platform and Culture
    - Experimentation Maturity Models
        1. Crawl: build up prerequisites/basic data science capabilities → compute summary stats; statistical testing; results meaningfully guide forward processes
        2. Walk: defining standard metrics/run more experiments → validating instrumentation; run A/A test; sample ratio mismatch test
        3. Run:running at scale → agree upon a set of metrics to codify an OEC that captures the trade-offs 
        4. Fly: automation; establish institutional memory - records of all previous experiments and changes, to learn from; improve culture of experiment
        
    - Factors
        - Leadership buy-in (especially crucial in the **Crawl** **and** **Walk** **maturity** **phases** to align the organization on goals): shared goals (goals in terms of improvements to metrics rather than shipping features) and high-level metrics, codifying trade-offs as steps to establish OEC, culture of failing fast (agility with short release cycles, healthy/quick feedback loop), review results, standard interpretation, transparency of decision making, a portfolio of high-risk/high-rewards projects relative to more incremental gain projects, support long-term learning over experiments,
        - **"Learning matters the most, not the results or whether we ship the change"** → full transparency on the experiment impact is critical, ways to achieve this
            - Compute many metrics, OEC, other related metrics are all on the dashboard to share
            - Send out messages about surprising results, meta-analysis over previous experiments to build intuition, to emphasize learning
            - Make it hard for experimenters to launch a Treatment if it impacts important metrics negatively (this last extreme can be counterproductive as it is better to have a culture where metrics are looked at and controversial decisions can be openly discussed).
            - Embrace learning from failed ideas to improve subsequent experiments
        - Components of a experiment platform
            - Experiment definition, setup, and management via a UI or application programming interface (API) and stored in the experiment system configuration
            - Experiment deployment, both server- and client-side, that covers variant assignment(Variant assignment is the process by which users are consistently assigned to an experiment variant, single-layer method, or concurrent experiments) and parameterization
            - Experiment instrumentation
            - Experiment analysis, which includes definition and computation of metrics and statistical tests like p-values.
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-14_at_5.17.58_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-14_at_5.17.58_PM.png)
                
    

**Part II Selected Topics for Everyone**

- Speed Matters - "Slow Down Experiment": an end-to-end Case Study
    - Key Assumption: local linear Approximation / first-order Taylor-series approximation
        - metric graph vs performance —> approximated by a linear line around the point matching today's performance
        - Assumption: if we were to move left of the vertical line (improving performance), the vertical delta on the left would be approximately the same as the one we measured on the right.
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled.png)
        
    - How to measure website performance - skipped
        
        
    - The slowdown experiment design
        
        where to insert the slowdown?
        
        how long should the delay be?
        
        - treatment effect to be larger so we can estimate "slope" more accurately
        - longer delay —> first-order Taylor approximation less accurate—>call for shorter delay
        - longer delay—> harm to users—>call for shorter delay
    - Impact of different page elements differs
        
        e.g. search results(critical) vs other areas like right pane(not that critical)
        
        "Perceived performance" estimate metrics: P189
        
        - Time to first result
        - Above the Fold time(AFT)e.g.percentage of pixels painted
        - Speed Index
        - Page Phase Time and User Ready Time
        
        one way to avoid coming up with definition for perceived performance : measure **time-to-users** action, e.g. click—> time-to-click/ time-to-successful click(avoid bait click), BUT required actions from users
        
    - Extreme Results
        
        LOL too fast may reduce user trust that some activity was done, so some products add fake progress bars
        
        "Trust level" to apply
        
- Organizational Metrics
    - Metrics Taxonomy
        
        
        - Goal Metrics (simple and stable): long term → What does **success look like** for your org? Missions?
        - Driver Metrics (aligned with the goal, actionable, relevant, sensitive, resistant to gaming): shorter term, faster moving, more sensitive → **drivers of success, some frames(HEART, AARRR...) or user funnels to break down the steps that lead to success** → right direction to success
        - Guardrail Metrics: usually more sensitive than GoalM & DM
            - Type 1: metrics protect the business → organizational guardrail metrics
                
                e.g. GoalM - increase registration; GuardrailM - per-user engagement 
                
            - Type 2: metrics assess the trustworthiness and internal validity of experiment results → trustworthiness guardrail metrics
        - Asset vs. Engagement metrics → accumulation of static assets; result of an action or usage
        - Business vs. Operational metrics → RPU or DAU (track the health of business); track operational concern (query-per-sec)
        - Data Quality metrics → internal validity and trustworthiness
        - Diagnosis / Debug metrics → help debugging a scenario where GM, DM, GM indicate issues → additional granularity or information (e.g. revenue indicator + conditional revenue metrics - avg → Did it increase/decrease because more/less people purchased or because the average purchase price changed?)
        
        **IMPORTANCE OF ALIGNING TEAM'S DRIVER METRICS WITH GOAL & STRATEGIC DIRECTION!!!**
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-17_at_12.05.18_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-17_at_12.05.18_PM.png)
        
    - Formulating Metrics: principles and techniques P199
        - Use hypotheses from **less-scalable methods** to generate ideas, and then validate them in **scalable data analyses** to determine a precise definition
            
            e.g. behavior pattern (less-scalable) → high-level metrics (scalable)
            
            e.g. user dissatisfaction correlated bounce rate
            
        - Quality concept in metrics, e.g. sign up and **engage**
        - Keep the stat model interpretable and validated over time
        - Easier to measure what you don't want → negative metrics as guardrail or debugging metrics
        - Metrics are proxies, e.g.CTR may lead to increased clickbait → create additional metrics
    - Evaluating Metrics
        
        Challenging → Establishing the **causal relationship of driver metrics to organizational goal metrics**, whether this driver metric really drives the goal metrics.
        
        - Validate Causality
            - Utilize other data source - surveys, focus groups, user experience research (UER)
            - Analyze observational data - invalidate hypothesis
            - Shared studies
            - Experiment with primary goal of evaluating metrics
            - Use historical experiments for evaluating new metrics
    - Evolving Metrics
        - Business evolved - new business lines, change of focus
        - Environment evolved - change of competition, public policies, user concerns
        - Understanding evolved - EVI
    - Additional Resources
        
        books reco
        
- Metrics for Experimentation & OEC
    - From Business Metrics to Metrics Appropriate for Experimentation
        
        metrics for experimentation:
        
        - measurable
        - attributable: be able to attribute metrics to experiment variants
        - sensitive and timely: sensitive enough to detect changes in a timely fashion. Sensitivity depends on the **statistical variance** of the underlying metric, **the effect size** (the delta between Treatment and Control in an experiment), and **the number of randomization units** (such as users)
    - Combing Key Metrics into an OEC
        - **OEC = weighted sum of the normalized metrics**
            
            Multiple metrics → normalize each metric to a predefined range(0-1), and assign each a weight. 
            
        - Limit the number of key metrics to 5
            
            The more metrics you have, the higher the chance that of null hypothesis(no difference is true) would be significant, causing potential conflicts or questions - p-hacking 1-(1-0.05)^k for k metrics
            
        
        Bing's Search Engine example: 
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-18_at_6.44.27_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-18_at_6.44.27_PM.png)
        
        - User per Month is determined in controlled experiment
        - Distinct queries per Session should be minimized but hard to measure, since decreasing might indicate abandonment
        - Session per User is key to optimize ← Satisfied users visit more often
        - Revenue per user should likewise not be used as an OEC for search and ad experiments without adding other constraints. **When looking at revenue metrics, we want to increase them without negatively impacting engagements metrics.** A common constraint is to restrict the average number of pixels that ads can use over multiple queries
        
        Amazon's email ads example: 
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-18_at_6.09.38_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-18_at_6.09.38_PM.png)
        
    - Goodhart's law, Campbell's Law and Lucas Critique
        
        correlation vs causality 
        
        relationship observed cannot be considered as structural or causal 
        
- Institutional Memory and Meta-analysis
    - what is institutional Memory?
        
        a digital journal of all changes through experimentation, documented meta data (key results, descriptions...)
        
    - what is meta-analysis
        
        mining data from all historical experiments
        
    - why it is useful?
        1. Solidify Experiment culture: highlight the importance of experimentation
        2. Encourage Experiment best practices: more people start to experiment, more commonly best practices are generated and followed
        3. Empower Future innovations: patterns emerge to guide better ideas
        4. Better understand and leverage Metrics: 
            1. metric sensitivity: Studying existing metrics by comparing their performance in past experiments allows you to identify potential long-term vs. short-term metrics
            2. related metrics: use the movement of metrics in experiments to identify how they relate to each other
            3. probabilistic priors for Bayesian approach: for matured products, it's reasonable to assume metric movement in historical experiments can offer reasonable prior distribution. This might not hold for product evolving rapidly
        5. Launch Empirical research: empirical evidence to evaluate and study theories through meta-analysis
- Ethics in Controlled Experiments P239
    - Background
        
        Experiments are conducted on people.
        
        Ethics is the set of rules or morals that govern what we should or should not do.
        
    - Key areas to consider
        1. Risk: physical, psychological, emotional, social, or economic.
        2. Benefits: direct or indirect (to users) 
        3. Provided choices
    - Data Collection Consent
    - Culture and Processes (fulfills the purpose of IRB)
    - User Identifier
        - Identified data is stored and collected with personally identifiable information (PII)
        - Anonymous data is stored and collected without any personally identifiable information
        - This data is considered **pseudonymous** if it is stored with a **randomly generated ID**, such as a cookie, that is assigned to some event, such as the first time a user opens an app or visits website and does not have an ID stored.
        
        for the data being gathered, collected, stored, and used in the
        experiment, the questions are:
        
        - How sensitive is the data?
        - What is the re-identification risk of individuals from
        the data?

**Part III Complementary and Alternative Techniques to Controlled Experiments**

- Complementary Techniques → to generate ideas to test, create, and validate metrics, and establish evidence to support broader conclusions
    - The Space of Complementary Techniques
        1. Idea generation and pruning
            
            easy-to-implement ideas → test directly by a controlled test
            
            expensive-to-implement ideas → use complementary techniques for early evaluation and pruning to reduce implementation cost
            
        2. Build reliable proxy metric
            
            E.g. To set a reliable proxy metric for user satisfaction (hard to measure) → e.g run a survey → analyze log data to see what large-scale observational metrics correlate with survey results
            
            **Depth of Information vs. Scale** (complementary techniques)
            
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%201.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%201.png)
        
    - Logs-based/Retrospective Analysis
        - Building intuition: what's the distribution like? difference across segs? change/shift over time?
        - Characterizing potential metrics - understand variance and distributions, correlation/comparison between existing metrics and new metrics, how a metric would potentially perform on past experiments
        - Generating ideas for A/B experiments based on exploring the underlying data
        - Natural Experiments - measure the effect of exogenous circumstances or bugs
        - Observational causal studies: when experiments are not possible → quasi-experiments, evaluate counterfactual effect, might lead to an improved inference
        
        **Limitation of conducting ONLY logs-based analysis:** These analyses can only infer what will happen in the future based on what happened in the past, but doesn't explain why it happened in the past 
        
        → **combine** logs-based analysis **with user and market research** gives a more comprehensive picture
        
    - Human Evaluation
        
        'rater' as additional metrics, raters are generally not end-users, calibrated labeled data
        
    - User Experience Research (UER) P265 read later
        
        A subset of field and lab studies that typically go deep with a few users, often by observing them doing tasks of interest and answering questions in either a lab setting or in situation. 
        
        → in-depth, intensive, direct observations, timely questions 
        
        → generating ideas, spotting problems, gaining insights 
        
        → validate using methods scaled to more users (observational analysis, controlled experiments)
        
    - Focus Groups
        
        Guided group discussion with recruited or potential users.
        
        - More scalable than UER, but less ground can be covered than UER.
        - Could fall prey to group-thinking and convergence on fewer opinions
        - What customers say in a focus group setting or a survey may not match their true preferences.
        
        Useful for getting feedback on ill-formed hypothesis on early-stage designing changes for future experiments, or for trying to understand underlying emotional reactions.
        
    - Surveys
        
        Recruit a population to answer a series of questions
        
        - quite challenging to design and analyze
            
            questions can be misinterpreted; answers are self-reported; population can be easily biased and may not be representative of the true user population
            
        
        Useful for observing trends over time on less directly-measurable issue, e.g. trust, reputation
        
    - External Data
        
        because you do not control the sampling or know the exact methods used to do the analysis, the absolute numbers may not always be useful, but **trends**, **correlations**, and **metric** **generation** and **validation** are all good use cases.
        
    - Putting It All Together
        
        tradeoff between depth of information and scale → depends on your goal/question
        
- Observational Causal Studies — P275 Read later
    - When Controlled Experiments Are Not Possible
        
        **Basic identity of causal inference**
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%202.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%202.png)
        
        *Comparison of the actual impact (what happens to the treated population) compared to the counterfactual (what would have happened if they had not been treated) is the critical concept for establishing causality*
        
    - Designs for Observational Causal Studies
        
        Estimate causal effect from observational studies → try to get as close to a causal result as possible
        
        - Challenges
            1. How to construct control and treatment groups for comparison
            2. How to model the effect given control and treatment groups
        - Interrupted Time Series (ITS)
            - Cannot randomize the Control and Treatment, use the same population for Control and Treatment
            - Vary the population experience over time → pre/post intervention
            
            A counterfactual estimated for the metric of interest by a model
            
            (after intervention) Treatment effect = the average difference between the actual values for the metric of interest and the counterfactual (those predicted by the model)
            
            Extension to ITS → **introduce** a Treatment and then **reverse** it, optionally **repeating** this procedure multiple times.
            
            - Issues
                1. Confounding effect: common confounds → seasonality, underlying system changes, user experience (e.g. when users notice the back-and-forth changes, inconsistency may irritate or frustrate users)
        - Interleaved Experiments Design
            
            To evaluate ranking algorithm changes, such as in search engines or search at a website.
            
            e.g. interspersing search results from different algorithms with duplicated results removed, one way to evaluate the algorithms would be to compare the click-through rate on results from the two algorithms → **Limitation**: the results must be homogenous, otherwise would introduce confounds 
            
        - Regression Discontinuity Design (RDD)
            
            Whenever there is a clear **threshold** that identifies the Treatment population → below the threshold as Control, above the threshold as Treatment. 
            
            Commonly applies when there's an algorithm that generates a score, and something happens based on a threshold of that score. 
            
            **Limitation**: confounding effect → threshold discontinuity might be contaminated by other factors that share the same threshold. 
            
        - Instrumented Variables (IV) and Natural Experiments
            
            IV is a technique that tries to approximate random assignment. 
            
            Some natural experiments are as good as random (e.g. monozygotic twins)
            
        - Propensity Scoring Matching (PSM)
            
            To construct comparable Control and Treatment population → **segmenting** the users by **common confounds,** similar to stratified sampling → To ensure that the comparison between Control and Treatment population is **not due to population mix changes**.
            
            Further implementation → instead of matching units on covariates, matches on a single number: a constructed propensity score 
            
            **Limitation**: confounding effect, confounding factors
            
        - Difference in Differences
            
            The Treatment effect is estimated as the **difference** in a metric of interest **minus** the **difference** **in** **Control** for that metric over the same period.
            
            ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-21_at_10.21.23_AM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-21_at_10.21.23_AM.png)
            
    - Pitfalls
        
        The main pitfall, regardless of method, in conducting observational causal studies is **unanticipated** **confounds** that can impact both the measured effect, as well as the attribution of causality to the change of interest.
        
        Another pitfall to be aware of are **spurious or deceptive correlations**. Deceptive correlations can be caused by strong outliers.
        
    - SIDEBAR: Refuted Observational Causal Studies

**Part IV Advanced Topics for Building an Experimentation Platform**

- Client - side Experiments
    - Differences between Server and Client Side
        1. Release Process
        - server-side → updating server-side code is as part of integration and deployment without interrupting the end-user experience; the variant is fully managed by server and no end-user action is required
        - client-side → if code on server side, similar to webpage; but there is a significant amount of code shipped with the client itself. Any changes to this code must be released differently, e.g. a mobile app release will involve 3 parties
        
        2. Data Communication between Client and Server
        
        The data connection between the client and server may be **limited or delayed** by:
        
        - Internet connectivity: internet accessibility
        - Cellular data bandwidth: cellular data plans, send telemetry data through wifi or cellular data, mobile infrastructure
        - Battery: low battery mode, battery consumption ↔ sending telemetry data
        - CPU, latency and performance: lower-end mobiles, frequency of data agg and sending data back-and-forth
        - Memory and storage: lower-end mobiles, caching
    - Implications for Experiments
        1. Anticipate Changes Early and Parameterize
        - A new app may be released before certain features are completed, in which case, these features are gated by configuration parameters, called **feature flags**, that turn the features off by default.
        - More features are built so they are **configurable** from the server side. This allows them to be evaluated in A/B tests, which helps both in measuring performance via controlled experiments, and also
        provides a safety net.
        - More fine-grained parameterization can be used extensively to add flexibility in creating new variants without needing a client release
        
        2. Expect a Delayed Logging and Effective Starting Time
        
        The limited or delayed data communication between client and server cannot only delay the arrival of data instrumentation, but also the start time of the experiment itself. The duration of an experiment may need to be extended to account for delays. Another important implication is that Treatment and Control variants may have a different effective starting times.
        
        3. Create a Failsafe to Handle Offline or Startup Cases
        
        4. Triggered Analysis May Need Client-Side Experiment Assignment Tracking → if the volume of these tracking events is high, it could cause latency and performance issues.
        
        5. Track Important Guardrails on Device and App Level Health
        
        6. Monitor Overall App Release through Quasi- experimental Methods
        
        7. Watch Out for Multiple Devices/Platforms and Interactions between Them
        
- Instrumentation
    - Client-Side vs. Server-Side Instrumentation
        
        **Client-side Instrumentation** → what the user experiences, including what they see and do
        
        - User actions: clicks, hovers, scrolls
        - Performance: time to load
        - Errors and crashes
        
        Drawbacks: 
        
        1)utilize significant CPU cycles and network bandwidth, impacting user experience → load time; 
        
        2)JavaScript instrumentation can be lossy P319 examples
        
        **System-side** → focuses on what your system does and why
        
        - Performance: time for server to generate response, which components take longest time
        - System response rate: how many requests servers received, how many pages served, retries handles
        - System information: how many exceptions or errors does the system throw? What is the cache hit rate?
    - Processing Logs from Multiple Sources
        - join logs: The ideal case is to have a common identifier in all logs to serve as **a join key**. The join key must indicate which events are for the **same user**, or randomization unit; join keys for specific events
        - **Shared formats** to make downstream processing easier: common fields(e.g., timestamp, country, language, platform) and customized fields
    - Culture of Instrumentation
        
        
- Choosing a Randomization Unit
    
    [Choosing your randomization unit in online A/B tests](https://ianwhitestone.work/choosing-randomization-unit/)
    
    - Randomization Unit and Analysis Unit
        - Granularity
            - page-level
            - session-level: a group of webpages viewed on a single visit, which is typically defined to end after 30 minutes of inactivity
            - user-level: All events from a single user is the unit. *`Note that a user is typically an **approximation** of a real user, with web cookies(some websites not requiring login) or login IDs typically used. Cookies can be erased, or in-private/incognito browser sessions used, leading to **overcounting**. For login IDs, shared accounts can lead to **undercounting**, whereas multiple accounts (e.g., users may have multiple e-mail accounts) can lead to **overcounting**.`*
        - Considerations
            
            1. How important is the **consistency** of the user experience? → whether users will notice the change
            
            - The more the user will notice the Treatment, the more important
            it is to use a **coarser granularity** in randomization to ensure the
            consistency of the user experience.
            
            2. Which metrics matter?
            
            - Finer levels → more units
                
                → **variance of mean** of a metric is **smaller**
                
                → the experiment will have **more statistical power** to detect small changes
                
                While a lower variance in metrics may seem like an advantage for choosing a finer granularity for randomization, some considerations to keep in mind:
                
                - If features act across that level of granularity, you cannot use that level of granularity for randomization.
                    
                    e.g. personalization or other inter-page dependences → invalid using page-views randomizations
                    
                - If metrics are computed across that level of granularity, then they cannot be used to measure the results.
                    
                    e.g. page-level randomization cannot measure impacts on total # of user session
                    
                - Exposing users to different variants will violated the stable unit treatment value assumption (Experiment units do not interfere with one another)
                
                In some enterprise scenarios, such as Office, tenants would like consistent experiences for the enterprise, limiting the ability to randomize by **user**. In advertising businesses that have auctions where advertisers compete, you could randomize by **advertiser** or by clusters of advertisers who are often competing in the same auctions. In social networks, you can randomize by **clusters of friends** to minimize interference 
                
        - Randomization Unit and Analysis Unit
            - Randomization Unit = Analysis Unit
                
                → easier to compute the variance 
                
                → based on reasonable independence assumption/identical distribution
                
                e.g. randomizing by page → CTR as metric analysis unit (clicks/pageviews)
                
                e.g. randomizing by user → sessions-per-user, clicks-per-user, and pageviews-per-user
                
            - Having the randomization unit be **coarser** than the analysis unit, such as randomizing by user and analyzing the click-through rate (by page) will work, but requires more nuanced analyses methods such as bootstrap or the delta method
                
                → switch to a user-based metric, e.g. click-through rate **per user**
                
        - User-level Randomization (the most common)
            
            Avoids inconsistent experience for the user and allows for long-term measurement such as user retention 
            
            - Considerations
                - **A signed-in user ID or login** that users can use across devices and platforms. Signed-in IDs are typically **stable** not just across platforms, but also longitudinally across time
                - A pseudonymous user ID, such as a **cookie**. These IDs are **not persistent across platforms**, so the same user visiting through desktop browser and mobile web would be considered two different IDs.
                - A **device ID** is an immutable ID tied to a specific device. Device IDs do not have the cross-device or cross-platform consistency that a signed-in identifier has but are typically stable
            - How to choose?
                
                Key aspects to consider is functional and ethical
                
                - Functional:
                    
                    main difference is scope (level of consistency); 
                    
                    longitudinal stability of the ID (e.g. goal is to measure where there is a long-term effect, latency or speed changes)
                    
                - Randomization at a **sub-user** level is useful only if there is no carrover or leakage
                - Using IP address is not recommended
                
- Ramping Experiment Exposure: trading off Speed, Quality and Risk
    - What is Ramping?
        - Exposure Control: Small exposure → large exposure
            
            Goes through a ramping process to **control unknown risks** associated with new feature launches (aka. controlled exposure).
            
        - Ramping up vs. down (for bad treatment)
    - Speed, Quality, Risk (SQR) Ramping Framework
        
        Purposes of running controlled experiments:
        
        - To **measure** the impact and ROI of Treatment if launched to 100%
        - To **reduce** risk when there's negative impact
        - To **learn** users reactions, ideally by segments, to identify potential bugs and inform future plans
    - Four Ramp Phases
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%203.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%203.png)
        
        - 1st Phase Pre-MPR: trade-off speed and risk → safely determine the risk is small and ramp quickly to the MPR
            
            Methods:
            
            - Create “rings” of testing populations and gradually expose the Treatment to successive rings to mitigate risk → first rings to get qualitative feedbacks → next rings may have quantitative measurement
                - Whitelisted individuals (to get feedbacks), such as the team implementing the new feature.
                - Company employees (forgiving on bad bugs)
                - Beta users or insiders who tend to be vocal and loyal, who want to see new features sooner, and who are usually willing to give feedback.
                - Data centers to isolate interactions that can be challenging to identify, such as memory leaks (death by slow leak) or other inappropriate use of resources (e.g. heavy disk I/O)
            - Automatically dialing up traffic until it reaches the desired allocation
                - The desired allocation → a particular ring or a preset traffic allocation %
            - Producing real-time or near-real-time measurements on key guardrail metrics.
        - 2nd Phase: MPR → dedicated to measure the impact of the experiment
            
            Recommendation to keep experiments at MPR for a week, and longer if novelty or primacy effects are present → still a diminishing return on precision after a week experimentation
            
            - capture time-dependent factors, e.g. rush hour/weekend
        - 3rd Phase: Post-MPR → should be no concerns regarding end-user impact/operational concerns
            
            Some concerns about increasing traffic load to some engineering infrastructures that may warrant incremental ramps before going to 100%. These ramps should only take a day or less, usually covering peak traffic periods with close monitoring.
            
        - 4th Phase: Long-term holdout/holdbacks or Replication
            
            (certain users do not get exposed to Treatment for a long time)
            
            Only apply long-term holdout when:
            
            - When the long-term Treatment effect may be different from the short-term effect → novelty or primacy effect; ensuring short-term effect is sustainable in a long term; adoption and discoverability
            - When early indicators show impact, but true-north metric is a long-term metric
            - When there's a benefit of variance reduction for holding longer
            
            When experiment result is surprising → A replication run reduces the multiple-testing concern and provides an unbiased estimate → Rerun the experiment with a different set of users or with an orthogonal re-randomization.
            
    - Post Final Ramp
        
        clean up the dead code path after launch
        
- Scaling Experiment Analysis
    - Data Processing
        1. sort and group the data → client/server side logs, e.g.user ID and timestamp
        2. clean the data → e.g. bots or fraud; too little/too many activities per session or in between; fix instrumentation issues or unexpected filtering 
        3. Enrich the data → add browser family and version by parsing a user agent raw string; day of week; annotation on whether to include this session, experiment transitions information...
    - Data Computation
        - Materialize per-user statistics(i.e., for every user, count the number of page-views, impressions, and clicks) and join that to a table that maps users to experiments.
        - Fully integrate the computation of per-user metrics with the experiment analysis, **where per-user metrics are computed along the way as needed** without being materialized separately → more flexible but requires additional work to ensure consistency across multiple pipeline
    - Results Summary and Visualization
        - Highlight key tests, such as SRM, to clearly indicate whether the results are trustworthy
        - Highlight the OEC and critical metrics, but also show the many other metrics, including guardrails, quality, and so on.
        - Present metrics as a **relative change**, with clear indications as to whether the results are **statistically significant**. Use color-coding and enable filters, so that significant changes are salient.
        - The visualization tool is not just for per-experiment results but is also useful for pivoting to **per-metric results across experiments.**
        
        Features to monitor for growing number of metrics 
        
        - Categorizing metrics into different groups, either by tier or function. For instance, LinkedIn categorizes metrics into three tiers: 1) Companywide 2) Product Specific 3) Feature Specific
        - Multiple testing—using p-value thresholds < 0.05
        - Metrics of interest: help to identify unexpected movement in some metrics
        - Relate metrics: e.g. CTR up could because click up or page-view down

**Part V Advanced Topics for Analyzing Experiments**

- The statistics behind Online Controlled Experiments
    - Two-Sample t-test
        
        Two-sample t-tests look at the size of the difference between the **two means relative to the variance**. The significance of the difference is represented by the p-value.
        The lower the p-value, the stronger the evidence that the Treatment is different from the Control.
        
        t-statistic T is normalized version of delta. 
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%204.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%204.png)
        
    - Two ways of checking statistical significance → p-value and Confidence Interval
        
        With t-statistic T, you can compute the p-value, which is the probability that T would be at least this extreme if there really is no difference between Treatment and Control.
        
        **P-value Interpretation**: *the probability of observing the delta if the Null hypothesis is true.*
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-24_at_5.48.40_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-24_at_5.48.40_PM.png)
        
        **Confidence Interval**: whether the confidence interval overlaps with zero.
        
        - A 95% confidence interval is the range that covers the true difference 95% of the time and has an equivalence to a p-value of 0.05;
        - the delta is statistically significant at 0.05 significance level if the 95% confidence interval does not contain zero or if the p-value is less than 0.05.
    - Normality Assumption
        
        (t-statistic T follows a normal distribution, a mean 0 and variance 1. The p-value is just the area under the normal curve)
        
        - Online controlled experiments usually have large sample size
            
            → while the sample distribution of Y does not follow normal distribution, the **average** Y usually does because of the **Central Limit Theorem**
            
        - One rule-of-thumb for the minimum number of samples needed for the average to have normal distribution is **355s^2** for each variant, s is **the skewness coefficient** of the sample distribution of metric Y
            
            ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%205.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%205.png)
            
        - Dealing with skewness of a metric → transform the metric or cap the values
            
            e.g. revenue metrics tend to have a high skewness coefficient
            
        - This rule-of-thumb provides good guidance for **when |s| > 1** but does not offer a useful lower bound when the distribution is symmetric or has small skewness. **Fewer samples are needed when skewness is smaller**
        - Test normality assumption:
            - offline simulation: randomly shuffle samples across Treatment and Control to generate **the null distribution** and compare with the normal curve using statistical tests such as Kolmogorov–Smirnov and Anderson-Darling
            - increase test sensitivity by only focusing on whether the Type I error rate is bounded by the preset threshold, for example, 0.05.
                
                if failed: permutation test to see where your observation stands relative to the simulated null distribution
                
    - Type I/II Erros and Power
        - **Type I error** is concluding that there is a significant difference between Treatment and Control when there is no real difference → rejecting null hypothesis when it's true
        - **Type II error** is when we conclude that there is no significant difference when there really is one.
            
            *Tradeoff: Using a higher p-value threshold means a higher Type I error rate but a smaller chance of missing a real difference, therefore a lower Type II error rate.*
            
            - **Power**: probability of detecting a difference between the variants (rejecting the null), when there really is a difference
                
                Power = 1 − Type II error
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-25_at_3.21.49_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-25_at_3.21.49_PM.png)
                
                - parameterized by delta, δ , the minimum delta of practical interest (the difference between Control and Treatment) → Many people consider power an absolute property of a test and forget that it is **relative to the size of the effect you want to detect**. Detecting smaller effect requires more power
                - at least **80%** power in our tests. It is common to conduct power analysis before starting the experiment to decide **how many samples are needed to achieve sufficient** power
                
                Sample size estimation given power:
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%206.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%206.png)
                
                *`σ2 is the sample variance, and δ is the difference between Treatment and Control (practical significance).`*
                
                - Sample size n → to estimate the required minimum sample size given practical significance to detect, use the **smallest δ** that is **practically significant** (also called the minimum detectable effect).
            - duration of the experiment (users visit over time) → impact actual sample size
            - trigger analysis (the value of variance and practical significance change when trigger conditions change)
            - for small sample size: important to calculate
                
                a) the probability of an estimate being in the wrong direction (Type S [sign] error)
                
                b) the factor by which the magnitude of an effect might be overestimated (Type M [magnitude] error or exaggeration ratio).
                
        
    - Bias
        
        When estimate and the true value is systemically different 
        
        → It can be caused by a platform bug, a flawed experiment design, or an unrepresentative sample such as company employee or test accounts.
        
    - Multiple Testing
        
        **“ Why is this irrelevant metric significant?”**
        
        **The Multiple Testing Problem** → When testing multiple things in parallel, the number of **false discoveries increases**
        
        - (simple & Conservative) Bonferroni Correction: a consistent but much smaller p-value threshold (0.05 divided by the number of tests)
        - (complex & less accessible) Benjamini-Hochberg procedure: varying p-value thresholds for different tests
        
        Alternative solution to the problem:
        
        - **Separate all metrics into three groups:**
        - First-order metrics: those you expect to be impacted by the experiment
        - Second-order metrics: those potentially to be impacted (e.g., through cannibalization)
        - Third-order metrics: those unlikely to be impacted.
        - **Apply tiered significance levels to each group** (e.g., 0.05, 0.01 and 0.001 respectively).
    - Fisher's Meta-analysis
        - Idea: combining results from multiple experiments that test on the **same** hypothesis.
        - Replication is done using either **orthogonal randomization** or **users who were not allocated to the original round of the experiment.**
        - Fisher: we can combine p-values from multiple independent statistical tests into one test statistic
            
            ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%207.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%207.png)
            
            pi is the p-value for the i-th hypothesis test. If all k Null hypothesis are true, this test statistic follows a **chi-squared distribution with 2k degrees of freedom**
            
        - Good for **increasing power and reducing false-positives** → if the experiment is still underpowered after all the power-increasing techniques (maximum power traffic allocation, variance reduction), try 2 or more (orthogonal) replications of the same experiment to achieve higher power by Fisher's Meta-analysis
- Variance Estimation and Improved Sensitivity P375
    - Common Pitfalls
        1. Delta vs. Delta% → variance of a delta% for estimate the CI
        2. Ratio Metrics (when analysis unit is different from experiment unit)
            - **Assumption (for metrics that meet this assumption)**: the samples (Y1,…, Yn) need to be i.i.d. (independently identically distributed) or at least uncorrelated. This assumption is satisfied if the analysis unit is the same as the experimental (randomization) unit.
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%208.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%208.png)
                
            - **When analysis unit is different from experiment unit:** For metrics e.g. CTR or revenue per click, the analysis unit is no longer per user but a page-view or click → variance computed using the simple formula above would be biased
                
                when **calculating variance of a ratio metric M as the ratio of “ average of user level metrics”** , M is normally distributed.
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-26_at_12.30.10_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-26_at_12.30.10_PM.png)
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-26_at_12.34.10_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-26_at_12.34.10_PM.png)
                
                In the case of delta %, since Control and Experiment is independent
                
                ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-26_at_12.35.39_PM.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Screen_Shot_2021-05-26_at_12.35.39_PM.png)
                
            - **For metrics that cannot be written in the form of ratio of 2 user-level metrics:** e.g. 90th percentile of page load time → **Bootstrap Method** → simulate randomization sampling with replacement and estimate the variance from many repeated simulations. (Even though bootstrap is computationally expensive, it is a powerful technique, broadly applicable, and a good complement to the delta method.)
        3. Outliers
            - Outliers are most commonly introduced by bots and spam behaviors clicking or performing many page-views.
            - A practical and effective method is to cap observations at a reasonable threshold
    - Improving Sensitivity/Power
        - By reducing **variance**
            - Create an evaluation metric with a smaller variance while capturing similar information
                
                e.g. var(number of searches) > var(number of searchers); 
                
                e.g. var(purchase amount) > var(purchase boolean)
                
                e.g. **var(purchasing spend) > var(conversion rate)**
                
            - Transform a metric through capping, binarization, or log transformation. For heavy long-tailed metrics, consider log transformation, especially if interpretability is not a concern(but maybe not the case for revenue)
            - Use triggered analysis → great way to remove noise introduced by people not affected by the treatment
            - Use stratification, Control-variates or CUPED
                - The common strata include platforms (desktop and mobile), browser types (Chrome, Firefox and Edge) and day-of-week... While stratification is most commonly conducted during the sampling phase (at runtime), it is usually expensive to implement at large scale. Therefore, most applications use post-stratification, which applies stratification retrospectively during the analysis phase.
                - Control-variates: uses covariates as regression variables instead of using them to construct the strata.
            - Randomize at a more granular unit (if the analysis unit is more granular): e.g. page level (but also have disadvantages: inconsistent user experience; impossible to measure any user-level impact over time)
            - Design a paired experiment: show the same user both Treatment and Control in a paired design, remove between-user variability and achieve a smaller variance → e.g. interleaving design
            - Pool Control groups: If you have several experiments splitting traffic and each has their own Control, consider pooling the separate controls to form a larger, shared Control group. Comparing each
            Treatment with this shared Control group increases the power for all experiments involved
    - Variance of Other Statistics
        
        When it comes to **time-based metrics**, such as page-load-time (PLT), it is common to use quantiles, not the mean, to measure site speed performance 
        
        → bootstrapping for conducting the statistical test to find the tail percentile
        
        → if the statistic follows a normal distribution asymptotically, the asymptotic variance for quantile metrics is a function of the density, by estimating the density, you can estimate the variance
        
- A/A test
    - Why A/A test?
        - Ensure that Type I errors are controlled (e.g., at 5%) as expected, checking for standard variance calculation, assumption of normality
        - Assessing metrics’ variability over time
        - Ensure that no bias exists between Treatment and Control users, especially if reusing populations from prior experiments; e.g. carry-over effect; residual effect
        - Compare data to the system of record
            
            (If the system of records shows X users visited the website during the experiment and you ran Control and Treatment at 20% each, do you see around 20% X users in each? Are you leaking users?)
            
        - Estimate variances for statistical power calculations for a given minimum detectable effect.
        - Examples:
            - Analysis Unit Differs from Randomization Unit P393
                - identified in A/A test when CTR was statistically significant far more often than expected 5% → randomizing by users and analyzing by pages → biased variance calculation if using "Count all the clicks and divide by the total number of pageviews"
            - Optimizely Encouraged Stopping when results are statistically significant: leading to many false positives
            - Browser redirects usually fails A/A tests with problems e.g. performance differences, bots, bookmarks/shared links cause contamination
            - Unequal percentages: uneven spilts → least recently used caches ; the rate of convergence to a Normal Distribution is different. e.g. if you have a highly skewed distribution, the Central Limit Theorem states that the average will converge to Normal, but when the percentages are unequal, the rate will be different. **In an A/B test, it’s the delta of the metric for Control and Treatment that matters, and the delta may be more Normal if the two constituents have the same distribution (even if not Normal).**
            - Hardware difference: small hardware difference can lead to unexpected differences of test results
    - How to run AA?
        
        Simulate a thousand A/A tests and plot the distribution of p-values. If the distribution is far from uniform, you have a problem.
        
        When the metric of interest is continuous and you have a simple Null hypothesis, such as equal means in our A/A test example, then the distribution of p-values under the Null should be uniform.
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%209.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%209.png)
        
         
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%2010.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%2010.png)
        
        Technique → "replay last week" with LRU (Least Recently Used) cache
        
        It's actually simulating A/A test: For each iteration, pick a new randomization hash seed for user assignment and replay the last week of data, splitting users into the two groups 
        
        → generate p-value for each metric of interest and plot histogram 
        
        → use a goodness-of-fit test check if distribution is close to uniform
        
    - When the AA fails?
        
        1. The distribution is skewed and clearly not close to uniform. 
        
        A common problem is a problem with **variance estimation** of metrics:
        
        - Is **the independence assumption** violated (as in the CTR example) because the randomization unit differs from the analysis unit? If so, deploy the delta method or bootstrapping
        - Does the metric have a **highly skewed distribution**? Normal approximation may fail for a small number of users. In some cases, **the minimum sample size** may need to be over 100,000 users. Capped metrics or setting minimum sample sizes may be necessary
        
        2.A large p-value indicates a problem with outliers → T-statistic would be smaller around 1 or -1, which maps p-value around 0.32 
        
        3. The distribution has a few point masses with large gaps. This happens when the data is single-valued (e.g., 0) with a few rare instances of non-zero values. ???
        
- Triggering for Improved Sensitivity
    - Examples of Triggering
        
        Intentional Partial Exposure: intentionally running on a segment of population
        
        Conditional Exposure: as soon as the users are exposed to a change, they triggered into experiment
        
        Coverage Increase: Treatment enlarges coverage for a feature. e.g. users between a range of purchase would see free shipping promotion
        
        Coverage Change: Treatment changes the coverage
        
        Triggering provides experimenters with a way to improve sensitivity (statistical power) by filtering out noise created by users who could not have been impacted by the experiment.
        
        - A change to checkout: only trigger users who started checkout
    - Optimal and Conservative Triggering
    - Overall Treatment Effect
        
        Diluted Impact/ Side-wide Impact → When computing the Treatment effect on the triggered population, you must dilute the effect for over-all user base.
        
        If you improved the revenue by 3% for 10% of users, did you improve your overall revenue by **10%*3% = 0.3%?** NO! **(common pitfall)**. **The overall impact could be anywhere from 0% to 3%!**
        
        There's no diluted effect when the user base is all triggered users and the only way of effect OEC is through triggering.
        
        2 ways of diluted percent impact??? (couldn't understand the equations)
        
        Note that **ratio metrics can cause Simpson’s paradox**, where the ratio in the triggered population improves, but the diluted global impact regresses.
        
    - Trustworthy Triggering
        - Sample Ratio Mismatch → if the overall experiment has no SRM, but the triggered analysis shows an SRM, then there is some bias being introduced.
        - Complement analysis → A/A test on never-triggered users, check for statistical significance
    - Common Pitfalls of Triggering
        - Experiment on tiny segments that are hard to generalize: the Amdahl's Law; except for the generalization of a small idea.
        - A triggered user is not properly triggered for the remaining experiment duration
        - Performance impact of counterfactual logging
    - Open Questions
- Sample Ratio Mismatch and Other Trust-related guardrail Metrics
    - Sample Ratio Mismatch: checking the ratio of units (e.g. users) between variants (Treatment & Control)
        
        check p-value → if p-value ≤ 0.05 → there's a sample ratio mismatch → bug in implementation
        
        Causes:
        
        - Buggy randomization of users:e.g. ramp up
        - Data pipeline issues
        - Residual effects
        - Bad trigger condition. The trigger condition should include any user that **could** have been impacted
        - 
    - Debugging SRMs
        - Validate that there is no difference upstream of the randomization point or trigger point
        - bot filtering
        - Exclude the initial period.
- Leakage and Interference between Variants
    
    Interference as a violation of SUTVA, sometimes called **spillover** or **leakage** between the variants
    
    **Direct Connections**
    
    social networks:
    
    Facebook Linkedin Skype calls
    
    **Indirect Connections**
    
    latent variables/shared same resources:
    
    - Airbnb
    - Uber/Lyft
    - eBay
    - Ad Campaigns(budget on a
    given campaign is shared between Treatment and Control groups)
    - Relevance Model Training
    - CPU
    - Sub-user experiment unit, e.g. page visit; session; Experiment units smaller than
    a user, such as a pageview, can cause potential leakage among units from the same user if there is a strong learning effect from the Treatment — mixed experience —may underestimate treatment effect
    - Examples
        
        Facebook/Linkedin
        
        Experiment units smaller than
        a user, such as a pageview, can cause potential leakage among units from the same user if there is a strong learning effect from the Treatment
        
    - Some practical Solutions
        - **Rule-of-Thumb: Ecosystem Value of an Action**
        
        "how much does a message from user A translate to visit sessions from both A and their neighbors? "
        
        One approach for establishing this rule-of-thumb is using historical experiments shown to have **downstream impact** and extrapolating this impact to the downstream impact of actions X/Y/Z using the Instrumental Variable approach
        
        - **Isolation:identifying the medium and isolating each variant**
            - Splitting shared resources
                - Can your interfering resources be split exactly according to the traffic allocation for your
                variants?
                - Does your traffic allocation (the resource split size) introduce bias? 50/50 is better option for traffic allocation then
            - Geo-based randomization:One caveat: randomizing at the geo level limits the sample size by the number of
            available geo locations. This leads to a bigger variance and less power for A/B tests.
            - Time-based randomization:One thing to keep in mind is that there is usually strong temporal variation, like the **day-of-week** or **hour-of-day** effects. This usually helps reduce variance by utilizing this information in paired t-tests or covariate adjustments
            - Network-cluster randomization:Similar to geobased randomization, on social networks, we construct “ clusters” of nodes that are close to each other based on their likelihood to interfere. We use each cluster as “ mega” units and randomize them independently into Treatment or Control groups
                - rare to have perfect isolation in practice
                - small effective sample size —> variance-bias tradeoff
            - Network ego-centric randomization:It
            achieves better isolation and smaller variance by creating clusters each comprised of an “ ego” (a focal individual) and its “ alters” (the individuals it is immediately connected to). This allows you to decide variant assignment for egos and alters separately
        
        Whenever applicable, always combine isolation methods to get a larger sample size. For example, while applying network-cluster randomization, **you can expand the sample size by leveraging time t as a sampling dimension.** If most of interference has a short time span and the Treatment effect itself is transactional, you can use a coin flip each day to determine variant assignment for each cluster
        
        Knowing that the **connection network** itself is usually **too dense to create isolated clusters,** identifying a subgraph where messages are likely to be exchanged can create better clusters.
        
        **Edge-level analysis**
        
        You can use Bernoulli randomization on users and then label the edges based on the experiment assignment of the users (nodes) as one of these four types: Treatment-to-
        Treatment, Treatment-to-Control, Control-to-Control, and Control-to- Treatment. Contrasting interactions (e.g., messages, likes) that happen on different edges, allows you to understand important network effects.
        
    - Detecting and Monitoring Interference
- Measuring Long-Term Treatment Effects
    - What are long-term effects?
        
        examples: P465
        
        The long-term effect is defined as the asymptotic effect of a Treatment, which, in theory, can be years out. Practically, it is common to consider long-term to be 3+ months, or based on the number of
        exposures (e.g., the Treatment effect for users exposed to the new feature at least 10 times).
        
    - Reasons that treatment effect may differ between shot-term and long-term
        - user-learned effects: users learn & adapt changes
        - network effects
            - social network:User behavior
            tends to be influenced by people in their network though it may take a while for a feature to reach its
            full effect as it propagates through their network
            - limited resources/two-sided market,e.g. Airbnb, eBay, Uber; hiring market, Linkedin's people you may know; increase Demand ←→ supply constraints: need time to catch up and sometimes it's limited —> a new feature may perform better at the beginning but may reach a lower equilibrium long term because of
            supply constraints
            - Delayed experience and measurement
            - Ecosystem change:launching other new features; seasonality; competitive landscape; government policies; concept drift; software rot
    - Why measure long-term effects?
        - Attribution:endigenous reason,e.g. user learned effect vs. exogenous, e.g. competitive landscape changes
        - Institutional learning: What is the difference between short term and long term? If the difference is sizable, what is causing it? If there is a strong
        novelty effect, this may indicate a suboptimal user experience.
        - Generalization
    - Long-running experiments
        
        keep an experiment running for a long time. You can measure the Treatment effect at the beginning of the experiment (in the first week) and at the end of the experiment (in the last week).
        
        ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%2011.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%2011.png)
        
        Limitation: 
        
        - Attribution: the longer the experiment runs, the more likely that a user will have experienced both Treatment and Control.e.g. change device; different cookie; leakage for network effect
        - Survivorship Bias: Not all users at the beginning of the experiment will survive to the end of the experiment. If the survival rate is different between
        Treatment and Control, pΔT would suffer from survivorship bias, which should also trigger an SRM alert
        - interaction with other new features
        - For measuring a time-extrapolated effect; exogenous factors
    - Alternative Methods for Long running experiments
        - Cohort analysis:One method is to select the cohort based on a stable ID, for
        example, logged-in user IDs. This method can be effective at addressing dilution and survivorship bias, especially if the cohort can be tracked and measured in a stable way P478
            - how stable the cohort is.e.g if ID is based on cookie and when cookie churn rate is high, then not work well
            - representative of overall evaluation; improve generalizability, e.g. weight adjustment based on stratification
        - Post-period analysis
            - turn off the experiment after it has been running for a while (time T) and then measure the difference between the users in Treatment and those in Control during time T and T + 1,'ramping up', both exposed to the exact same features
                - learning effect:
                    - user-learned effect;
                    - system-learned effect; the system may have "remembered" information from Treatment period.
            - Time-staggered Treatments
            
            measure the difference between the two versions of Treatment.
            
            ![TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%2012.png](TRUSTWORTHY%20ONLINE%20CONTROLLED%20EXPERIMENTS%20473191b630b94508801b25af85e24700/Untitled%2012.png)
            
            This method assumes that the difference between the two Treatments grows smaller over time. In other words, T1(t) – T0(t) is a decreasing function of t. While this is a plausible assumption, in practice, you also need to ensure that there is enough time gap between the two staggered
            Treatments
            
            - Holdback and Reverse Experimement
                - holdback:keeping 10% of users in
                Control for several weeks (or months) after launching the Treatment to 90% users
                - reverse:we ramp 10% of users back into the Control several weeks (or months) after launching the Treatment to 100% of users
