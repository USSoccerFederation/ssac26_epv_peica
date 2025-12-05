<div align="center"><h2>GraphEPV and PEICA: Graph Neural Network Expected Possession Value and Player Evaluation through Individual Credit Attribution in Soccer via Sports-Specific Shapley Coalitions</h2></div>


### Introduction
In this research, we introduce GraphEPV, a graph neural network architecture that predicts the probability of scoring a goal within the next 10 seconds, and PEICA, a custom sports-specific Shapley method for player evaluation through individual credit attribution. This approach allows us to derive the moment-to-moment impact of each player throughout a game as it relates to their team's objective of scoring or preventing goals.

---

### Methods

#### Graph Neural Network Expected Possession Value
We train, test and validate GraphEPV using 63 matches of [**public** World Cup 2022 tracking and event data](https://drive.google.com/drive/folders/1_a_q1e9CXeEPJ3GdCv_3-rNO3gPqacfa), where each graph represents a single frame of positional data. Data from the final is set aside for further validation. Despite the limited number of goals in our dataset, our model achieves a Precision-Recall AUC of 0.0643, an 11x improvement over random guessing.

#### PEICA: Player Evaluation through Individual Credit Attribution
To quantify individual player contributions to their team’s objective, we employ a Shapley method where we generate masked graph variants per frame. For each variant, a random subset of players is masked using the average values of a different random subset of teammates. This team-aware masking strategy preserves the underlying graph structure while systematically removing individual player influences. We then make predictions on these randomly adjusted graphs using GraphEPV. By comparing predictions across masked coalitions, we uncover each player's contribution to the predicted probability of scoring or preventing a goal within the next 10 seconds.

In Figure 1, we can clearly identify individual player contributions throughout the possession sequence. 
It depicts the end position (and prior movements) of a possession sequence with relevant moments annotated (1-8). 

<div align="center">
  <img src="assets/peica.png" alt="PEICA Image" width="600">
  <p><strong>Figure 1.</strong> A sequence of play from the 2022 World Cup final, highlighting individual player contributions to <strong>attacking team (Argentina)</strong> and <strong>defensive team (France)</strong> objectives. Ball follows dotted line.</p>
</div>

---

#### Results
We validate PEICA by comparing player total scores of ten different possession sequences (see Table 2) to standardized expert ratings (μ<sub>rater</sub>) from ten U.S. Soccer Youth National Team Head Coaches and Performance Analysts. These ratings are given on a 5-point Likert scale using anonymized tracking data videos from the final, one per possession sequence. Our ten raters achieve an Intraclass Correlation Coefficient (ICC) of 0.967 and their average ratings have a Spearman’s rank correlation of 0.536 with PEICA. Additionally, we compare our results to an event data framework that values on-ball actions by estimating scoring probabilities (VAEP) [Decroos 2019 et al.] to show a tremendous increase in both quality and quantity of insights, interpretability and granularity gained when using PEICA (see Table 1).



<div align="center">
<table>
  <thead>
    <tr>
      <th>#</th>
      <th>Player</th>
      <th>PEICA</th>
      <th>μ<sub>rater</sub></th>
      <th>VAEP</th>
    </tr>
  </thead>
  <tbody>
    <tr style="background-color: #e91e63; color: white;">
      <td colspan="5"><strong>Argentina</strong></td>
    </tr>
    <tr>
      <td><strong>10</strong></td>
      <td>L. Messi</td>
      <td>2.57</td>
      <td>1.15</td>
      <td>0.032 <sup>[1,2]</sup></td>
    </tr>
    <tr>
      <td><strong>3</strong></td>
      <td>N. Tagliafico</td>
      <td>1.78</td>
      <td>0.48</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>20</strong></td>
      <td>A. Mac Allister</td>
      <td>1.46</td>
      <td>0.55</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>9</strong></td>
      <td>J. Alvarez</td>
      <td>1.40</td>
      <td>0.31</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>11</strong></td>
      <td>A. Di Maria</td>
      <td>1.34</td>
      <td>0.98</td>
      <td>0.024 <sup>[2]</sup></td>
    </tr>
    <tr>
      <td><strong>26</strong></td>
      <td>N. Molina</td>
      <td>0.76</td>
      <td>0.31</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>13</strong></td>
      <td>C. Romero</td>
      <td>0.73</td>
      <td>0.68</td>
      <td>0.008 <sup>[1,2]</sup></td>
    </tr>
    <tr>
      <td><strong>7</strong></td>
      <td>R. de Paul</td>
      <td>-0.08</td>
      <td>0.46</td>
      <td>0.021 <sup>[1,2]</sup></td>
    </tr>
    <tr>
      <td><strong>24</strong></td>
      <td>E. Fernandez</td>
      <td>-0.18</td>
      <td>-0.45</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>19</strong></td>
      <td>N. Otamendi</td>
      <td>-1.03</td>
      <td>-0.18</td>
      <td>0.003 <sup>[1]</sup></td>
    </tr>
    <tr>
      <td><strong>23</strong></td>
      <td>E. Martinez</td>
      <td>-10.90</td>
      <td>-1.10</td>
      <td>-</td>
    </tr>
    <tr style="background-color: #2196f3; color: white;">
      <td colspan="5"><strong>France</strong></td>
    </tr>
    <tr>
      <td><strong>9</strong></td>
      <td>O. Giroud</td>
      <td>0.02</td>
      <td>-0.79</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>1</strong></td>
      <td>H. Lloris</td>
      <td>-0.17</td>
      <td>0.98</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>5</strong></td>
      <td>J. Kounde</td>
      <td>-0.22</td>
      <td>0.06</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>18</strong></td>
      <td>D. Upamecano</td>
      <td>-0.27</td>
      <td>0.66</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>22</strong></td>
      <td>T. Hernandez</td>
      <td>-0.30</td>
      <td>0.54</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>4</strong></td>
      <td>R. Varane</td>
      <td>-0.32</td>
      <td>0.66</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>14</strong></td>
      <td>A. Rabiot</td>
      <td>-0.36</td>
      <td>0.22</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>10</strong></td>
      <td>K. Mbappe</td>
      <td>-0.36</td>
      <td>-1.03</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>8</strong></td>
      <td>A. Tchouameni</td>
      <td>-0.73</td>
      <td>0.28</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>11</strong></td>
      <td>O. Dembele</td>
      <td>-0.82</td>
      <td>-0.59</td>
      <td>-</td>
    </tr>
    <tr>
      <td><strong>7</strong></td>
      <td>A. Griezmann</td>
      <td>-1.47</td>
      <td>-0.02</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

<p><strong>Table 1.</strong> PEICA, the average standardized rating (μ<sub>rater</sub>) and VAEP (on-ball events only: [1] pass, [2] carry) for the possession sequence shown in Figure 1. Spearman's rank correlation between PEICA and μ<sub>rater</sub> for this example is 0.61.</p>

</div>

---

#### Conclusion
PEICA allows us to evaluate player performance by directly quantifying each player's added value towards offensive or defensive team objectives, valuing both traditional measurable actions and previously unquantifiable tactical elements like tracking back, support runs, and other on and off-ball behaviors.

This approach enables in-depth, data-driven player evaluation, scouting, and tactical analysis through consistent, automated analysis. The model's strong correlation with expert judgment validates its practical reliability while providing objective quantifications of every player's contribution.

Our work addresses a significant gap in sports analytics and is applicable to other invasion sports (e.g., American football, basketball, and hockey).

---

### Benchmark

To encourage reproducibility and to facilitate researchers to benchmark their model outputs against the insights of expert soccer practitioners, we share these 10 segments (see Table 2) as:
- [Tracking data and Event data](benchmark/segments.ipynb)
- [Anonymized top-down positional tracking data videos](benchmark/videos/1.mp4).
- [Aggregated standardized expert grades, and PEICA, VAEP and AtomicVAEP values for these 10 segments](benchmark/benchmark.csv). Within this file `anon_player_id` refers to the players in the anonymized videos.

<div align="center">
<table>
  <thead>
    <tr>
      <th>Segment</th>
      <th>Start Time</th>
      <th>End Time</th>
      <th>Period</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>16:07</td>
      <td>16:15</td>
      <td>1</td>
    </tr>
    <tr>
      <td>2</td>
      <td>12:47</td>
      <td>13:07</td>
      <td>1</td>
    </tr>
    <tr>
      <td>3</td>
      <td>20:38</td>
      <td>20:45</td>
      <td>1</td>
    </tr>
    <tr>
      <td>4</td>
      <td>34:00</td>
      <td>34:14</td>
      <td>1</td>
    </tr>
    <tr>
      <td>5</td>
      <td>13:15</td>
      <td>13:19</td>
      <td>2</td>
    </tr>
    <tr>
      <td>6</td>
      <td>16:36</td>
      <td>16:54</td>
      <td>2</td>
    </tr>
    <tr>
      <td>7</td>
      <td>17:15</td>
      <td>17:24</td>
      <td>2</td>
    </tr>
    <tr>
      <td>8</td>
      <td>17:56</td>
      <td>18:04</td>
      <td>2</td>
    </tr>
    <tr>
      <td>9</td>
      <td>33:06</td>
      <td>33:12</td>
      <td>2</td>
    </tr>
    <tr>
      <td>10</td>
      <td>35:48</td>
      <td>35:59</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<caption>Table 2. Ten segments from the FIFA 2022 World Cup final between Argentina and France. Videos, ratings and raw event and tracking data for these segments is avaible in this GitHub repository.</caption>
</div>