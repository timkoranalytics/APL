# APL
Applied Linear Models Project (SAS)

A student runs a two-factor experiment to test how microwave power and temperature affect popping. The student chooses three levels of Power (low, medium, and high) and two Times (low and high), running one bag at each condition. The student counts the number of uncooked kernels as the response variable.

So, the student runs an experiment to test four different popcorn brands, recording the number of kernels left unpopped measuring batches of each brand 4 times, using the same popcorn popper and randomizing the order of the brands. 

Questions to be answered:

What are the null and alternative hypotheses?

How many degrees of freedom does the Treatment Sum of Squares have? How about the Error Sum of Squares?

Assuming that the conditions required for ANOVA are satisfied, what is the P-value? What would you conclude?

What else about the data would you like to see in order to check the assumptions and conditions?

From the interaction plot, do the effects appear to be additive? 

Does the F-test in the ANOVA table support your conclusion in? 

What would you recommend to the student to make the perfect popcorn?



Part 1. ANOVA task

Step 1. Uploading data:

%web_drop_table(WORK.IMPORT);

FILENAME REFFILE '/home/u64102526/MIDTERMPROJ/popcorn_data.xlsx';

PROC IMPORT DATAFILE=REFFILE

DBMS=XLSX

OUT=WORK.IMPORT;

GETNAMES=YES;

RUN;

PROC CONTENTS DATA=WORK.IMPORT; 
RUN;

%web_open_table(WORK.IMPORT);

Step 2. Building model:

PROC GLM data=work.import PLOT = DIAGNOSTICS;

 class Time Power;
 
model Percent_Not_Edible_Kernels = Time Power Time*Power;

run;

Step 3. Results of the model and answers to the question:

3.1. Hypotheses:

H0: Power and Time do not significantly affect the percentage of uncooked
grains.

H1: There is a significant effect of at least one factor(Power or Time) on the
number of uncooked grains.

3.2. Degrees of freedom Treatment SS and Error SS:

![image](https://github.com/user-attachments/assets/a3c3a0de-88d3-4054-a5a6-19a046d666bc)

From the table we can see that:
Treatment Sum of Squares - 5
Error Sum of Squares - 39 

3.3. P-values of factors and their interaction:

![image](https://github.com/user-attachments/assets/3a7228a2-7b13-484c-8a14-cca0935fb726)

Before studying the interaction effect, let's look at our factors independently.
P-value for Time is 0.0017 (<0.05), it is statistically significant, which means
that the time of cooking popcorn significantly affects the percentage of
uncooked grains. Thus, we reject the null hypothesis.
P-value for Power is 0.4315 (>0.05) indicating that power of the microwave does
not significantly affect the percentage of uncooked grains.
Now let's look on p-value of interaction of our factors (Time*Power): it is 0.0226
(<0.05), and it is statistically significant, indicating that interaction of
Time and Power have a statistically significant effect on the percentage of
unpopped grains. Thus, we may also reject the null hypothesis. 

3.4. Assumptions: 

![image](https://github.com/user-attachments/assets/9cf7064d-b3b7-4042-815f-c5ecebd6a0e5)

The graphs below help us to check the assumptions of the anova test. It’s clearly
seen that the distribution of residuals is normal. Q-Q plot also demonstrates that
observations are along the diagonal line, however there are some deviations on
the tails. So we would say that the assumptions of normality are almost satisfied.
According to the conditions of the experiments we would say that
independence is most likely satisfied, however there are some potential issues:
for example, the student used the same microwave for each experiment, which
leaves a space for potential dependence (residual heat), since we cannot be
sure that the student cooled the microwave after each experiment.
Homoscedasticity is also almost satisfied. We can see that residuals are
approximately uniformly distributed around zero, but it’s also notable that in the
center the spread of observations is smaller than on the edges. The Fit-Mean
Residual plot also demonstrates residual lines are uniform with some outliers
on the edges. Thus, there are minor deviations but not crucial. 

3.5. Interaction effect:

![image](https://github.com/user-attachments/assets/e3e22e4e-45ba-4ed2-9656-2015b478fed7)

According to the interaction plot, our effects are not additive. It's clearly seen
on the graph that lines are not parallel, indicating that there is an interaction
between factors of our interest. For example, the "high power" line has a
slightly different negative slope compared to the "medium power" line, while
the "low power" line in contrast shows a positive slope. It also can be supported by the fact
that interaction of our effects appeared to be statisticaly significant (0.0226 < 0.05).

![image](https://github.com/user-attachments/assets/f8f3e471-99c3-4072-8a2d-937b4187a36f)

3.6. What would you recommend to the student to make the perfect popcorn? 

According to the interaction plot, to achieve a minimum percentage of unсooked
grains the best choice would be Medium Power and Low Time. 

![image](https://github.com/user-attachments/assets/3553dd65-d9b5-4b8a-948e-d8fc4082cba9)


