# PH-Balancing Component
<p> A short summary of the development of a Ph-balancing component of a vaccine reactor developed alongside the EEE Cohort of UCL. The project was developed using C and the Arduino IDE to control the Microcontroller, along with the Processing 3 Graphics Library for User Interface. This document will not contain any code, but instead highlights the practical challenges faced when developing the Ph-balancing component. The tolerable pH range of our system was pH 6 to pH 8.</p>

<h2> Programmer Tunnel-Vision </h2>
<p> Often when we work as Software Developers, the kind of problems we encounter are purely virtual - one would just often need to observe the results and debug their code to locate their problem. However, in an interdisciplinary project where there can be considered many phases and translations to a real-world output, things tend to get more complex. It often pays to be extremely observant and analytical as erroneous results can stem from many aspects. It could potentially be a programming error or a logic in the programming (which we know how to handle) but now problems can stem from virtual to physical translation or it could potentially be a physical error. The document will outline the problems that we ran into. </p>

<h2> Quick to React </h2>
<p> The logic on paper was straightforward - if the solution is too acidic, drip alkaline into the solution through the alkaline motor, and if it was too alkaline, we would drip acid via the acid motor. However, what we found was that the Ph was not homogenous - our observation was that frequently there would be a 'spike' in the Ph reading very briefly which would set off the motors when unecessary. This very much could be an erroneuous reading, or that we did not give enough time for the solutions to mix and so the program would need to be adjusted to ignore this small spike. </p>

<p> As our Software subdivision immediately requested the EEE subdivision to install more Ph sensors so we could take multiple readings to determine an average, the EEE subdivision had to remind us that we were not made of money and that we had to work with only one Ph sensor. And so the solution (the answer, not the liquid we are neutralising) was to split the usual reading of 2 seconds to 4 readings every 0.5 seconds and determine an average. With this logic implemented, the program was less prone to these spikes.</p>

<h2> Tug-Of-War </h2>
<p> As we developed the prototype, we had aimed to keep the solution as neutral as possible, with the acid and alkaline motors trigerring periodically to keep the solution neutral. However, what we had was a situation in where one of the motors were constantly functioning, and immediately after one of them would stop functioning, the other would trigger and this process will repeatedly happen, until one of the acid or alkaline solutions were depleted. Very naively, we had simply assumed "the range of the tolerable Ph is too narrow" and changing this could potentially kill the vaccine, but for testing purposes we had widened it anyway and to our surprise, the situation remained.</p>

<p> After some careful consideration, this problem stemmed from oversights of both subdivisions - the software developers had run under the assumption that Ph would change immediately, and the EEE had designed the physical system with pipes coming from above, meaning that acid or alkaline could still drip into the system even after the motors had stopped working. Therefore, the EEE subdivision had realtered the design so that the pipes came in horizontally rather than verically and the programmers had introduced a small 'grace period' to allow the solutions to mix and reread the Ph before deciding to add more acid or alkaline. The tolerable Ph range was then reverted and the system was working as intended.</p>

<h2> Overshooting </h2>
<p> Soon after the tug-of-war problem we moved onto a larger prototype. With the acid or alkaline had been introduced in our system, the logic indicated that the solution should be close to neutral (pH 7). However, what we found out was that it would typically overshoot to the opposite side (so when we introduced acid, the pH would jump from pH 6 to pH 9 and when we introduced alkaline, the pH would jump from about pH 9 to pH 5, potentially killing our vaccine). As we had just made adjustments for the ToW problem, we had assumed we were responsible for introducing the error and immediately sought to adjust the 'grace period', but to no avail, the system would always overshoot the desired pH. </p>

<p> It wasn't until one of the EEE members had pointed out the simple flaw that we were possibly introducing too much acid/alkaline at a given time in our system. A simple problem that could be resolved with minutes had set us back 2 days. With this in mind, we sought to adjust the functionality of the motor. The motor logic indicated that we could not control the power of the motor - it would simply be on [1] or off [0], and so we had to introduce intermittent delays in turning it on and off to simulate the 'power' of a motor. This eventually solved our problem.</p>

<h2> Summary </h2>
<p> Real world scenarios that require interdisciplinary teamwork can be very confusing and require observation and good communication between each discipline. It also often pays not to jump to the first conclusion and to highlight potential problems and short-comings in all aspects of a system. In very time-constrained situations, it also pays to measure twice and cut once. </p>




