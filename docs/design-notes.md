# Design notes: why a pseudo-rigid leg

Short notes on the reasoning behind the leg architecture, kept at the level of approach rather than implementation.

## The problem with the two obvious extremes

A stiff-legged quadruped is well understood: rigid links, a servo at each joint, inverse kinematics, a trot or a crawl. It carries load well and is easy to control. What it cannot do is take hold of the environment. On a flat floor it is excellent; against a pipe, a ledge, a railing or the inside of a cluttered space, a rigid foot can only press.

A fully soft limb is the opposite. It conforms, it wraps, it distributes contact pressure, and it survives collisions. What it cannot do is carry a heavy body or hold a pose precisely, because it has no rigid reference and its stiffness changes with pressure.

## The split used here

The leg is split so that each part does the job it is good at:

- **The joint is rigid.** A serial-bus servo provides a stiff, measurable, repeatable root angle. The body's weight and the leg's orientation are carried by a component with a known torque limit rather than by pressurised silicone.
- **Everything below the joint is soft.** A multi-chamber pneumatic body bends under pressure and conforms to whatever it is wrapped around. Reinforcement on the outside of the body makes it bend in a controlled direction rather than balloon.
- **The soft segment is where grip comes from.** The useful behaviour in a tight space is not stepping-on but wrapping-around: the leg closes on geometry and uses that contact instead of relying on friction from a flat pad.

## Chamber arrangement

Two arrangements were compared during concept work: chambers stacked along the leg (bending in one plane) and chambers arranged around the leg (bending in a controllable direction, and able to close around a form). The ring arrangement is the one that supports wrapping. Both exist as concept geometry; neither has been characterised on the bench yet.

## What is honestly unresolved

- No bench measurement exists yet for bend angle against pressure, blocked force, response time or fatigue life.
- The soft segment's stiffness when unpressurised, and what that does to the standing pose, is an open question.
- Wrap performance on real geometry (pipe, rail, ledge) is untested. Until it is measured, "tight-space manoeuvring" is a design target, not a result.

## Simulation position

MuJoCo carries the model that the IK is validated against, and standing was the first trained behaviour. Soft continuum compliance is not fully represented in the current model, so the simulator is used for kinematics and gross dynamics rather than for predicting wrap performance.
