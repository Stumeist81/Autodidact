# Building Ghost in the Machine: Why I’m Creating an AI That Codes Itself (Starting with Tic-Tac-Toe)

The purpose of this project is to build a system where LLM technology is used to train Neural Networks with minimum user input. This project will utilise Generative AI and CI/CD. The question I am asking is *Can an AI build, test, and evolve its own successor from scratch?*

I have decided to name this **Project: Autodidact** which in basic terms means "A self taught person".

It is going to start with with a simple implementation of the game of Tic-Tac-Toe (well actually it starts with me staring at a blank screen, wondering what I am doing with my life). Once I have a basic system working for Tic Tac Toe, I aim to evolve this to Chequers, as much as I would like
to explore Chess, I feel that is not only beyond my capability but also beyond my respource limit.

> **A Quick Note on the Journey:** 
> Just to set expectations: this is a long-term passion project, and progress will be intentionally slow. More importantly, this entire venture is my sandbox for learning the ins and outs of **Agentic Workflows, CI/CD Pipelines, and Grafana observability**. Expect plenty of broken code, late-night debugging, and figuring things out as I go! I can honestly give no expectations here on timelines.

---

## The Sandbox: Where It All Begins

Why Tic-Tac-Toe? Basically I want to start with something simple. By starting with a solved game, I can focus entirely on the *meta-architecture*. As much as I would like to start with Chequers, I know that is too much for now.

The foundation kicks off with a classic pairing:
* A deterministic **Minimax** algorithm (acting as the baseline gatekeeper).
* A foundational **Neural Network** trying to find patterns beyond raw brute force.

Ideally, from there onwards the Generative AI will take care of the rest (I am well aware that this is a very ambitious project)

**NOTE:**
>I originally debated whether to train against Minimax directly or just let two Neural Networks evolve by playing each other. The cleanest approach, I believe, is to use both, but for separate jobs:

>Training via Self-Play (NN vs NN): The Neural Networks play against copies of themselves to generate their own game data and learn board dynamics. This keeps the training loop self-contained without needing human datasets or complex external training data.

>Grading via Minimax (Candidate vs Minimax): Minimax acts purely as the benchmark in the Arena. Because Tic-Tac-Toe is a solved game, Minimax cannot lose—a perfect play always ends in a win or a draw. A new candidate model only gets promoted to "Champion" if it can consistently hold its own (achieve 0 losses) against Minimax across the 99-round tournament.

---

## The Evolutionary Engine

Autodidact isn't just about training a model; it's about building a self-sustaining ecosystem of specialized AI agents. Here is how the pipeline works:

1. **The Scavengers:** I initially wanted to develop some webscrapers that would search the internet, review technical papers regarding AI and use these as a basis for the next version of the Neural Network. I have decided that this is probably a bit too ambitious, so I plan to have a
txt file which I will manually fill with headings for the AI to utilise. For example, for the minimax implementation, one of these headings might be "Alpha Pruning", the GenAI will take one of these heading at a time and (attempt to) implement them.
2. **The Architects:** Using the supplied headings/keywords, agentic models rewrite sections of the AI’s codebase, trying new strategies, reward functions, or network architectures. I am well aware this can and will get very messy.
3. **The Arena:** The new implementation will face off against the previous "champion", my current idea is a 99 round match (odd number so no 50/50 wins) to determine the "best model".
4. **The Post-Mortem:** Reviewer agents analyze the logs of every game, pointing out tactical blunders and feeding insights back to the Architect agents for the next iteration. This part of the system is still very much in  my head, I am going to need to create some sort of review system, that only picks and highlights one issue to the "Architects"

---

## The Infrastructure (Or: Letting Go of the Wheel)

To make this work without making me bankrupt, I am going to use as many guard rails as possible. 

* **No Direct Control:** The AI agents write code, but they deploy it into strictly defined, sandboxed container environments. They have no direct access to the underlying infrastructure—up to a point. (Later phases MIGHT introduce multi-container setups to test how these AI systems handle distributed networking and scaling). Although I know agentic systems can use Terraform/Bicep/etc, I am not willing to go that far (just yet).
* **The Cloud Backbone:** An agentic workflow handles the orchestration, automation, and deployment pipeline (likely leveraging Azure, as I use it daily at work). 
* **The Data Lake:** Every single move, game state, and match result is logged into a NoSQL database, creating a massive historical archive of the AI's evolutionary tree. I am also considering having an Agent that will write a blog post on each major change made. 

---

## Observability & What's Next

As for observing this system, I will be looking to utilise Grafana dashboards, so that performance and game metrics can be tracked. This will also be utilised by the Agents so they can ideally spot any bottlenecks or immediate areas that need improvement.

Just to clarify, this document may change over time due to the progress of the project. 

---

