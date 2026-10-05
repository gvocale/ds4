# Agent guide

## Agent turn discipline (all repos, INFRA-233)

An agent session only acts while a turn is open. Ending a turn on a promise ("next I will...", "continuing", "now running X") with nothing running leaves nothing to wake the session, and work silently stops.

A turn may end in exactly one of three states:

1. The next step's tool call has already been made in this same turn.
2. A background job with notify-on-complete is running, and its completion will wake the session (say what it is and what happens with the result).
3. You are blocked on the owner (say plainly what you need).

Run long jobs in the background with a hard time limit; a foreground command over about 5 minutes is a bug. Do not say work is done, running or verified unless a tool result in this session shows it. Worklists live on a Plane card with a timestamped comment per step; a worklist with no new comment for 30 minutes is a stall.
