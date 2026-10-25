# SNHU-CS230-by-Jonathan-Burton
Project submission for SNHU's CS230 Course.

# CS-230 Operating Platforms: The Gaming Room Software Design Document

This repository holds the software design document I put together for **The Gaming Room** in CS-230 Operating Platforms. Below is a reflection on the project and what I took away from it.

---

## Client Summary and Requirements

The client was **The Gaming Room**, a company with an Android game called *Draw It or Lose It*. Teams race to guess what a drawing shows before the 30-second timer runs out. They wanted to take it from Android-only to a web-based game that could run on multiple platforms.

Their main requirements were:

- A game can have one or more teams, and each team can have multiple players
- Game and team names have to be unique so users can check if a name is already taken
- Only one instance of the game service can exist in memory at a time
- Every game, team, and player needs a unique id

I designed a Java-based solution around those requirements and built a working prototype to go with it.

## What I Did Well

I think the Recommendations section is my strongest work. I didn't just recommend Linux. I explained why Ubuntu Server LTS would be a good fit for the game. It's free to license, works well with Java, and would let The Gaming Room maintain one back end for multiple platforms. I also recommended PostgreSQL for permanent storage, Redis for live game data, and WebSockets for real-time updates.

I'm also happy with how I addressed the prototype's limitations. In the Design Constraints section, I pointed out that the GameService singleton could create duplicate ids or names if multiple users accessed it at the same time. I also explained how the current in-memory storage would lose data after a server restart. Recognizing those problems helped me make better recommendations for storage and scaling later in the document.

## How the Design Document Helped With Coding

The UML diagram was basically my blueprint. Before I wrote any Java, I already knew Entity would hold the shared id and name, that Game, Team, and Player would inherit from it, and where the singleton and iterator patterns belonged. So when I built the prototype, I had a clearer idea of what I needed to build instead of figuring out the structure as I went. It also made it easier to catch when my code started drifting from the requirements.

## What I Would Revise

If I could revise one part, it'd be the System Architecture View. It wasn't required for this project, so I left it blank. But by the end, my recommendations described a whole system: browsers and mobile clients, a load balancer, multiple Linux servers, PostgreSQL, Redis, and cloud storage for images. I'd add a system architecture diagram showing how all of those connect and where data flows. Right now the reader has to piece that picture together from several sections, and one diagram would make it easier to understand for both the client and the dev team.

## Interpreting the User's Needs

I read the client's needs as two groups: the people playing the game and the company running it. Players need a fair, smooth round no matter what device they're on, which is why I kept the timer and guess checks on the server and planned for reconnects when someone's connection drops. The company needs something it can actually support. They mentioned their staff didn't know how to set up the environment, so I kept the design simple and documented, and I recommended Ubuntu LTS partly because it doesn't need constant OS upgrades.

Considering the user matters because software can work fine technically and still fail if it doesn't fit how people use it. Coming from a pharmacy background, I've seen that firsthand. A tool is only as good as how well it fits the person using it.

## My Approach to Software Design

I started with the requirements and mapped each one to a piece of the design. Checking for duplicate names led to the iterator pattern, the requirement for one game service led to the singleton, and shared attributes led to the Entity base class. Then I looked at constraints like network speed, many users at once, and memory, and let those shape the platform recommendations.

For a similar project in the future, I'd keep that requirements-first approach and add a few things. I'd talk with stakeholders earlier to clear up vague requirements, build in thread safety from the start instead of flagging it as a later fix, and sketch the full system architecture early so every later decision has a big picture to fit into.

---

**Contents of this repository:**

- `Software_Design_Doc_Completed.docx` – the completed design document for The Gaming Room
- `README.md` – this reflection
