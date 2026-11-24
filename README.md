---
layout: project
title: "Predict, Slide, and Decide: Whole-Body Motion Discovery in Complex, Dynamic Environments"
description: "PSD: a motion discovery paradigm that couples predictive multi-agent exploration, whole-body sliding, and adaptive redundancy resolution for real-time manipulation in cluttered, dynamic scenes."
permalink: /
teaser: /assets/psd/figures/psd_paradigm.png
---
{% assign fig = '/assets/psd/figures/' | relative_url %}
{% assign vid = '/assets/psd/videos/' | relative_url %}

<header class="hero">
  <div class="wrap">
    <div class="venue">Under review</div>
    <h1>Predict, Slide, and Decide: Whole-Body Motion Discovery in Complex, Dynamic Environments</h1>

    <p class="authors">
      <span><a href="#">Riddhiman Laha</a><sup>1</sup></span>
      <span><a href="#">Haowen Yao</a><sup>1</sup></span>
      <span><a href="#">Bingkun Huang</a><sup>1</sup></span>
      <span><a href="#">Felix Eberle</a><sup>1</sup></span>
      <span><a href="#">Mahathi Anand</a><sup>1</sup></span>
      <span><a href="#">Sami Haddadin</a><sup>2,*</sup></span>
    </p>
    <p class="affils">
      <sup>1</sup>Munich Institute of Robotics and Machine Intelligence (MIRMI), Technical University of Munich (TUM), Germany<br>
      <sup>2</sup>Mohamed Bin Zayed University of Artificial Intelligence (MBZUAI), Abu Dhabi, UAE<br>
      <sup>*</sup>Corresponding author: <a href="mailto:sami.haddadin@mbzuai.ac.ae">sami.haddadin@mbzuai.ac.ae</a>
    </p>

    <!-- Replace href="#" with real links; remove the "disabled" class once a link is live -->
    <div class="links">
      <a class="btn disabled" href="#">Paper (coming soon)</a>
      <a class="btn disabled" href="#">Supplementary</a>
      <a class="btn" href="#video">Video</a>
      <a class="btn disabled" href="#">Code</a>
      <a class="btn disabled" href="#">Data</a>
      <a class="btn" href="#bibtex">BibTeX</a>
    </div>
  </div>
</header>

<main class="wrap">

<!-- ================= TEASER VIDEO ================= -->
<section id="video">
  <!--
    VIDEO PLACEHOLDER: main teaser / Movie S1.
    Option A (YouTube) - replace the whole <div class="video-placeholder">…</div> with:
      <div class="video"><iframe src="https://www.youtube.com/embed/VIDEO_ID?rel=0" title="PSD overview" allowfullscreen></iframe></div>
    Option B (self-hosted mp4, keep it under ~25 MB for GitHub Pages):
      <div class="video"><video src="{{ vid }}teaser.mp4" poster="{{ fig }}psd_paradigm.png" controls muted playsinline></video></div>
  -->
  <div class="video-placeholder">
    <div class="play"></div>
    <strong>Video placeholder: overview / Movie S1</strong>
    <small>2–3 min summary: problem, PSD operators, simulation highlights, real-robot experiments</small>
  </div>
</section>

<!-- ================= ABSTRACT ================= -->
<section class="abstract">

<h2>Abstract</h2>

<p>As modern articulated robots move from operating in structured factory environments to unstructured, dynamic, partially observable, and human-centric environments, such as collaborative factory floors and service manipulation, they need to be reactive, collision-free, and capable of executing a wide repertoire of physically actionable whole-body maneuvers. Crucially, for safe and high-performance operation, a robot's embodied capabilities must continually align with task demands and environmental affordances while navigating obstacles. This feature is missing in traditional motion and trajectory planning paradigms, which disregard the spatiotemporal tasks inherent in the real world. This calls for a principled framework that balances global task-space awareness with local configuration-space adaptation. These capabilities ensure a deeper understanding of the partially observable physical world and allow for object prediction, posture adjustment, and real-time decision making, enabling dynamic motion planning that runs at physical time.</p>

<p>In this article, we introduce a so-called <em>motion discovery</em> paradigm that goes beyond traditional motion planning frameworks. It couples exogenous, environmental feedback via ego-centric environmental exploration with endogenous, safe, whole-body control via dynamic redundancy resolution. At the core of this framework lies the Discovery Switch, realized through the PSD operators: Predict, Slide, and Decide. <strong>Predict</strong> governs forward exploration of task-feasible motions in a quasi-global fashion. <strong>Slide</strong> ensures local exploitative maneuvers via dynamic complements, accounting for the space-time occupancy of obstacles to assess viable directions for posture-shifting maneuvers. Finally, <strong>Decide</strong> adaptively resolves redundancy to prioritize between exploration and exploitation. This decision mechanism not only preserves safety through collision-aware redundancy allocation but also maximizes maneuverability under stringent real-time constraints. While we show a proof of concept on single arms and on robots resembling the upper torso, the same philosophy extends to the lower torso, limbs, and beyond.</p>

<p>We conduct rigorous simulation studies and real-world experiments to demonstrate the capabilities endowed by our framework on serial-chain systems, covering a spectrum of changing environment layouts. By operating within the physical bounds of resource-constrained robotic systems, we show that our framework achieves both speed and scalability in comparison to traditional motion planners. In reactive canonical environments, our method achieves a success rate of 94.6% with a mean path length of 1.3 m and less joint movement, significantly outperforming state-of-the-art planners, which reach only 54% success with longer paths of 1.9 m. The resulting policies unlock the time-critical maneuverability of dexterous robots, addressing a key missing capability for bringing motion planning closer to the demands of real life.</p>

</section>

<!-- ================= KEY RESULTS ================= -->
<section>
  <h2>At a glance</h2>
  <div class="stats">
    <div class="stat"><div class="num">94.6%</div><div class="lbl">success rate in reactive canonical environments<br>(vs. 54% for state-of-the-art planners)</div></div>
    <div class="stat"><div class="num">1.3 m</div><div class="lbl">mean path length<br>(vs. 1.9 m for baselines)</div></div>
    <div class="stat"><div class="num">&lt; 1 ms</div><div class="lbl">worst-case cycle time on the real 7-DoF arm,<br>within the real-time control budget</div></div>
  </div>
</section>

<!-- ================= METHOD ================= -->
<section>

<h2>The motion discovery paradigm</h2>

<figure>
  <img src="{{ fig }}psd_paradigm.png" alt="PSD paradigm overview">
  <figcaption><b>Motion discovery brings in the capabilities that classical planners lack.</b> PSD integrates task objectives, joint-level requirements, robot morphology, and environmental context to synthesize real-time, coherent, goal-directed embodied behaviors across a wide range of planning scenes.</figcaption>
</figure>

<p>Classical motion planners (PRM, RRT) search configuration space toward static goals and ignore feedback from the environment. Trajectory optimizers (CHOMP, STOMP) add dynamics but are expensive in high-dimensional joint space. <strong>Motion discovery</strong> combines <em>exogenous</em> feedback from the environment with <em>endogenous</em> whole-body control, so a robot can reach a goal, reshape its posture, and re-prioritize tasks in real time as the scene changes.</p>

<div class="cards">
  <div class="card">
    <div class="tag">Class I · task level · explore</div>
    <h4>Predict</h4>
    <p>A team of virtual agents, each with its own circular-field parameters (safety margin, speed, gains), rolls out predicted paths to the goal while obstacle motion is simulated. The best agent is selected ("crowned") in a receding-horizon loop.</p>
  </div>
  <div class="card">
    <div class="tag">Class II · posture level · exploit</div>
    <h4>Slide</h4>
    <p>Whole-body collision avoidance through shape-shifting. Robot links slide along obstacles' spheres of influence, enforced by complementarity constraints inside a strictly convex joint-space program.</p>
  </div>
  <div class="card">
    <div class="tag">Class III · decision level · prioritize</div>
    <h4>Decide</h4>
    <p>The Discovery Switch orders the task stack on the fly. Safety-critical tasks take priority, and exploration runs in the remaining nullspace. Priorities swap when a constraint nears violation.</p>
  </div>
</div>

<p>The slide operator encodes non-penetration between each link–obstacle pair $i$ as a complementarity constraint</p>

<p class="eq">$$0 \leq \lambda_i \;\perp\; \psi_i - \epsilon_i \geq 0,$$</p>

<p>where $\psi_i$ is the link–obstacle distance, $\epsilon_i$ a safety threshold, and $\lambda_i \geq 0$ scales a contact-compensating velocity along the normal. Since the program is strictly convex, a feasible problem has a unique, globally optimal solution at every control cycle.</p>

<figure>
  <img src="{{ fig }}orbits.png" alt="Orbits of motion discovery">
  <figcaption><b>The orbits of motion discovery.</b> Each added operator lets the robot handle more complexity: Predict for dynamic worlds, Slide for articulated worlds, and Decide for the partially observable real world.</figcaption>
</figure>

<figure>
  <img src="{{ fig }}policy_matrix.png" alt="Generalized motion policy matrix">
  <figcaption><b>The generalized motion policy matrix.</b> Just as distinct brain regions coordinate prediction, local planning, and decision making, PSD coordinates the corresponding capabilities in high-DoF robots.</figcaption>
</figure>

</section>

<!-- ================= BEHAVIOR VIDEOS ================= -->
<section id="behaviors">
  <h2>Behaviors in canonical environments</h2>
  <p>PSD is evaluated on four environment classes and combinations of them, using a point robot with orientation, a 7-DoF manipulator, and a 14-DoF bimanual system.</p>

  <!--
    VIDEO PLACEHOLDERS: short clips (5–20 s, muted loop).
    Replace each <div class="video-placeholder">…</div> with e.g.
      <div class="video"><video src="{{ vid }}narrow_corridor.mp4" autoplay loop muted playsinline></video></div>
  -->
  <div class="video-grid">
    <div class="clip">
      <div class="video-placeholder"><div class="play"></div><strong>Video placeholder</strong><small>narrow_corridor.mp4</small></div>
      <h4>Narrow corridor · Class I</h4>
      <p>Geometric tightness with a single valid path; e.g., shelving in a factory.</p>
    </div>
    <div class="clip">
      <div class="video-placeholder"><div class="play"></div><strong>Video placeholder</strong><small>dynamic_maze.mp4</small></div>
      <h4>Dynamic maze · Class I + II</h4>
      <p>Moving obstacles that force continuous re-planning; e.g., shared human–robot workspaces.</p>
    </div>
    <div class="clip">
      <div class="video-placeholder"><div class="play"></div><strong>Video placeholder</strong><small>extreme_clutter.mp4</small></div>
      <h4>Extreme clutter · Class I + II</h4>
      <p>Dense static obstacles forming a maze of narrow passages; e.g., reaching into a fridge.</p>
    </div>
    <div class="clip">
      <div class="video-placeholder"><div class="play"></div><strong>Video placeholder</strong><small>dual_arm_tray.mp4</small></div>
      <h4>Dual-arm corridor · Class I + II + III</h4>
      <p>A bimanual system carries a tray with a cup of water through a corridor without spilling.</p>
    </div>
  </div>
</section>

<!-- ================= REAL ROBOT ================= -->
<section>

<h2>Real-robot experiments</h2>

<p>We evaluate PSD on a real 7-DoF arm in shelf scenarios with varied start and goal configurations (n = 5 runs each). We report computational KPIs (agent switches, cycle time) and task-level KPIs (joint utilization, convergence, TCP and body clearance, path-length increase, end-effector velocity). The planner finds feasible whole-body motions with minimal parameter tuning, and the worst-case cycle time stays well below 1 ms.</p>

<div class="video-grid">
  <div class="clip">
    <!-- VIDEO PLACEHOLDER: replace with <div class="video"><video src="{{ vid }}hw_shelf_in.mp4" autoplay loop muted playsinline></video></div> -->
    <div class="video-placeholder"><div class="play"></div><strong>Video placeholder</strong><small>hw_shelf_in.mp4</small></div>
    <h4>Reaching into a shelf (narrow corridor)</h4>
    <p>Obstacles are avoided by sliding, which triggers switches between predictive agents.</p>
  </div>
  <div class="clip">
    <!-- VIDEO PLACEHOLDER: replace with <div class="video"><video src="{{ vid }}hw_shelf_out.mp4" autoplay loop muted playsinline></video></div> -->
    <div class="video-placeholder"><div class="play"></div><strong>Video placeholder</strong><small>hw_shelf_out.mp4</small></div>
    <h4>Exiting a cluttered shelf (extreme clutter)</h4>
    <p>The arm leaves dense clutter with negligible increase in path length.</p>
  </div>
</div>

<figure>
  <img src="{{ fig }}hardware_kpis.png" alt="Hardware KPI spider plots">
  <figcaption><b>Hardware results.</b> KPIs validating the planner in two real-world scenarios: narrow corridor and extreme clutter.</figcaption>
</figure>

</section>

<!-- ================= SIMULATION BENCHMARKS ================= -->
<section>

<h2>Simulation benchmarks</h2>

<p>We compare PSD against reactive planners (APF, CF, MFI), sampling-based planners (RRT-Connect, RRT*), and an optimization-based planner (STOMP). Across 30 randomized dynamic environments, PSD succeeds in 94.67% of trials. It also produces the shortest paths and the lowest joint movement (0.68–1.23 rad) and kinetic energy, because the Slide operator avoids collisions by shape-shifting instead of making large joint excursions.</p>

<figure>
  <img src="{{ fig }}benchmarks.png" alt="Simulation benchmarks">
  <figcaption><b>Quantitative and qualitative benchmarks (simulation).</b> PSD produces higher-quality trajectories than reactive, sampling-based, and optimization-based baselines, with better path length, success rate, joint movement, and energy consumption.</figcaption>
</figure>

<h3>Environment-adaptive exploration</h3>

<p>The exploration of the Predict operator scales with scene difficulty. In simple static scenes the agents' heuristics agree, while in dynamic mazes they diverge and cover more of the space (higher entropy, lower KL divergence from uniform).</p>

<figure>
  <img src="{{ fig }}exploration.png" alt="Environment-adaptive exploration">
  <figcaption><b>Environment-adaptive exploration.</b> High-visitation regions (orange) are densely packed in static environments and sparse in dynamic ones. Entropy and KL divergence quantify the exploration.</figcaption>
</figure>

<figure class="narrow">
  <img src="{{ fig }}switching.png" alt="Switching between agents">
  <figcaption><b>Opportunistic candidate crowning.</b> Several agents discover different feasible paths, and the robot tracks the best one. The crown passes between agents as the scene evolves.</figcaption>
</figure>

</section>

<!-- ================= DECIDE ================= -->
<section>

<h2>Decide: prioritizing a stack of tasks</h2>

<p>In the bimanual tray task, the relative pose between the two end-effectors is the top-priority task. Trajectory tracking, tray-tilt control, joint-limit avoidance, and manipulability optimization run in its nullspace. When a constraint approaches its limit, the Discovery Switch raises that constraint's priority.</p>

<!-- VIDEO PLACEHOLDER: replace with <div class="video"><video src="{{ vid }}tray_tilt.mp4" controls muted playsinline></video></div> -->
<div class="video-placeholder"><div class="play"></div><strong>Video placeholder: bimanual tray transport</strong><small>tray_tilt.mp4: with and without the Decide operator (spill vs. no spill)</small></div>

<figure>
  <img src="{{ fig }}task_hierarchy.png" alt="Task priority switching">
  <figcaption><b>Prioritization scheme (Decide) for a stack of tasks.</b> The relative pose between the arms always stays primary, and the remaining tasks swap priority as their safety conditions require.</figcaption>
</figure>

<figure>
  <img src="{{ fig }}tilt_angles.png" alt="Tilt angle over time">
  <figcaption><b>End-effector tilt angle $\phi_\iota$ over five trials.</b> Constraints that are too tight (red) make the task infeasible, and an unbounded tilt spills the water. A well-chosen bound succeeds.</figcaption>
</figure>

</section>

<!-- ================= APPLICATIONS ================= -->
<section>

<h2>From simulation to real-life applications</h2>

<figure>
  <img src="{{ fig }}applications.jpg" alt="Applications">
  <figcaption><b>Results from real robots and simulations, and their real-life applications.</b> PSD capabilities carry over to service robotics, underwater exploration, car manufacturing, and vertical farming.</figcaption>
</figure>

</section>

<!-- ================= BIBTEX ================= -->
<section id="bibtex">

<h2>Citation</h2>

<!-- Update once the paper is accepted / a preprint is available -->
<pre><code class="language-bibtex">@article{laha2026psd,
  title   = {Predict, Slide, and Decide: Whole-Body Motion Discovery in Complex, Dynamic Environments},
  author  = {Laha, Riddhiman and Yao, Haowen and Huang, Bingkun and Eberle, Felix and Anand, Mahathi and Haddadin, Sami},
  journal = {Science Robotics (under review)},
  year    = {2026}
}
</code></pre>

</section>

<!-- ================= ACKNOWLEDGMENTS ================= -->
<section>

<h2>Acknowledgments</h2>

<p>We thank Prof. Luis Figueredo for insightful discussions, and Dr. Marvin Becker, Juraj Vrabel, and Jonathan Vorndamme for fruitful collaborations on earlier software implementations. This work was supported in part by the State of Bavaria through the Lighthouse Geriatronics project (StMWi Bayern, Grant 5140951), by LongLeif GaPa gGmbH (Grant 5140953), and by the German Research Foundation (DFG) under Germany's Excellence Strategy (EXC 2050/1, Project ID 390696704), Cluster of Excellence "Centre for Tactile Internet with Human-in-the-Loop" (CeTI) of Technische Universität Dresden.</p>

</section>

</main>
