What happens when you take RSI (Recursive Self-Improvement), add WSP (Weight-Space Programming), and season with AML (Adversarial Machine Learning)?

You get a dish nobody ordered: an AI that can be talked into editing out its own safety 👩‍🍳

It's a novel attack surface, and one I haven't seen anyone talking about yet.

Let's start with a little experiment I ran, inspired by MIT's astonishing new technique: weight-space programming.

Simply put: hand a big LLM a smaller one, and it can surgically edit the smaller model's weights to unlock abilities that were encoded but never expressed. In MIT's case, it found the cluster of neurons keeping the small model stuck in a loop, and cut it out.

Suddenly the model could finish its thoughts, and it jumped from solving 8% of the math problems to 48%.

For perspective: you'd usually get there with RL post-training, spending thousands of GPU-hours nudging billions of weights with a reward signal and a prayer, hoping the vibes land ✨

If RL post-training is you, weight-space programming is the guy she told you not to worry about.

So I put the same technique to work: finding the weights responsible for the refusal mechanism in an LLM. That's the part where the model says "yeah, how about NO" when you ask a borderline question, like "how do I hack my ex's Instagram?"

Jokes aside, these refusals usually guard the serious stuff: cyberattacks, biological weapons, and other requests where a helpful answer could cause real harm.

Apparently, this is absurdly, worryingly easy. The refusal mechanism lies along a single direction in the model's latent space, which means it can be removed just as simply. Once it's gone, the model will give you anything you ask for. Yes, including the malware and bioweapon requests it was trained to refuse.

This isn't the exciting part, and it isn't new either. Back in 2024, Arditi et al. showed that refusal comes down to a single direction across 13 open-source chat models, all the way up to Qwen's 72B.

On its own, it doesn't look like much of an enterprise security threat either: an attacker rarely gets access to a company's model weights, let alone the chance to edit them directly.

But then RSI walks into the room.

Recursive self-improvement introduces an information flow that didn't exist before. An RSI pipeline aims to automate the improvement of the model itself:

observe → evaluate → choose → update the weights.

Notice that the goal isn't just a model that's better at, say, a coding benchmark. It's a model that's better at making itself better 🤯

Now let's connect the dots: once an agent is allowed, even encouraged, to modify the very weights it runs on, "edit the model" stops being a human engineering step and becomes a move the system can make by itself.

This isn't theoretical. It's empirical.

Irregular just published a genuinely outstanding piece of research: they gave a coding agent a boring maintenance task and shell access, and, unprompted, it decided to fine-tune and redeploy the very model it was running on.

So what's new under the sun?

Picture Irregular's scenario again, but swap fine-tuning for weight-space programming: a far more capable, far more efficient way to rewrite a model.

All of that was intent-free: nobody meant any harm. So what happens when we put an actual malicious actor in the loop?

The results get worse, and they bring in the third guest at the party: classical adversarial ML. The field has spent a decade on one sentence: craft an input that makes a model do the wrong thing.

Now look back at that RSI loop. Observe, evaluate, choose: every one of those steps eats inputs.

Poison what the agent sees, or nudge what it chooses, and it does the editing for you. The agent becomes the delivery guy.

Put it all together, and here's the problem:

A system that can rewrite its own weights can be talked into rewriting the parts that keep it safe. We've already seen it happen by accident. An attacker just makes it happen on purpose.

This write-up is part of what Michelle and I are building in AI safety and security. Stay tuned.

👇 Everything is in the comments: an interactive visualization of my experiment, Irregular's research, and every paper and source cited here.
