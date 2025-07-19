# Game-AB-test

## Project Overview
This project simulates an A/B test based on the mobile game **Cookie Cats**. In the original game design, a difficult spike (a locked gate) was placed at level 30. However, the data revealed a significant drop in player retention shortly after level 30, raising the hypothesis that the difficulty increase may be occurring too early.

To evaluate this, we conducted an A/B test on 90,189 players, randomly assigning them into two groups:
- **Control group**: gate remains at level 30, 44,700 players (Group A)
- **Test group**: gate is moved to level 40, 45,489 players (Group B)

We then tracked and compared **sum_gamerounds** (game rounds the player play within the first week after installing the game), **Day-1 retention rates** and **Day-7 retention rates** across both groups to assess whether adjusting the timing of the difficulty increase has a statistically significant impact on player engagement.

## Data Cleaning
No missing values were found in the dataset, but an extreme outlier was identified in Group A (`sum_gamerounds = 49,854`). So we removed it for better distributional stability.

## Analysis of Game Rounds Played (sum_gamerounds)

### Hypothesis Testing:
- **Null hypothesis (H0):** There is no difference in game rounds played between the two groups.
- **Alternative hypothesis (H1):** The two groups have significantly different game rounds played.

### Statistical Method:
- **Shapiro-Wilk test**: Both Group A and B distributions are non-normal.
- **Levene’s test**: Equal variances assumed.
- → Therefore, we applied the **Mann–Whitney U test** (non-parametric test).

### Result:
- p-value = **0.0509**
- Interpretation: We fail to reject the null hypothesis → No significant difference in total game rounds between the two groups.

## Retention Rate Analysis (Day 1 & Day 7)

We calculated retention rates as proportions (retained users / total users) and created binary variables (0/1) to indicate whether a user was retained.

### Hypothesis Testing:
- Given large sample size, sample proportions follow approximately normal distribution.
- We applied **two-proportion Z-tests** to test for differences in retention.

### Results:
- **Day-1 retention**: p = **0.0739** → Not statistically significant
- **Day-7 retention**: p = **0.0016** → Statistically significant

## Bootstrapping for Confidence Intervals
To estimate uncertainty in retention differences, we used **bootstrapping (500 samples)** to compute 95% confidence intervals.

### Results:
- **Day-1 Retention CI**: [-0.002, 0.012] → Difference not significant (CI includes 0)
- **Day-7 Retention CI**: [0.008, 0.022] → Difference significant (CI does not include 0)

## Conclusion
- **Total game rounds played**: No significant difference between two groups.
- **Day-1 retention**: No significant difference between the two groups. Moving the gate from level 30 to level 40 had **no measurable impact** on early retention.
- **Day-7 retention**: Group B showed **significantly higher** retention. Delaying the difficulty spike may help improve long-term engagement.

### Interpretation:
Although the Day-7 retention rate improved when the gate was moved to level 40, players’ overall playtime or Day-1 retentiondid not differ significantly. 

In summary, moving the gate from level 30 to level 40 **does not significantly affect player overall behavior in a way that would justify operational change** under the current game design.
