# About the Dataset

The Mafia Dataset was created to model the behavior of deceptive actors in the context of the Mafia game, as described in the paper “Putting the Con in Context: Identifying Deceptive Actors in the Game of Mafia”. We hope that this dataset will be of use to others studying the effects of deception on language use.

# About the Dataset Collection Methodology

A total of 460 participants were recruited from Amazon Mechanical Turk using the experiment platform Dallinger (http://github.com/dallinger/Dallinger). Between 4 and 10 participants were recruited for each Mafia game: 1 to 2 participants were designated mafia, and the rest were bystanders. Forty-four of these Mafia games are included in this dataset. Participants were paid $2.50 for completing the task, plus bonuses for time spent waiting for other participants to arrive in a chatroom to begin the experiment (waiting was paid at $5.00/hour).

Upon recruitment, participants were shown an instructional video and accompanying transcript describing how to play the text-based Mafia game. After they completed a quiz demonstrating they understood the information, they entered a waiting room until the desired number of participants was reached. Participants were then assigned a role (mafioso or bystander) and fake name, after which they began playing the game. 

The game dynamics were as follows. Each mafia member was aware of the identities of their fellow mafia members and thus, by process of elimination, knew the identities of the bystanders. However, the bystanders did not know the true membership affiliations of anyone else in the game. The goal of the mafia was to eliminate bystanders until the number of mafia was greater than or equal to that of the bystanders. The goal of the bystanders was to identify and eliminate all of the mafia members. The game proceeded in phases, alternating between nighttime and daytime (Figure 1). During the nighttime, mafia members could secretly communicate to decide on who to eliminate, after which they discretely voted, and the person with the majority vote was eliminated from the game. If there was a tie, one of the people involved in the tie was randomly chosen to be eliminated. During the daytime, everyone was made aware of who was eliminated during the nighttime, and then all players could openly communicate to decide who to eliminate. All the players then voted publicly, and the person with the majority vote was eliminated and announced to be a bystander or mafioso. Thus, during the nighttime mafia could secretly communicate and eliminate any node in the network, whereas during the daytime mafia could participate in the voting and communication protocols in the same way as bystanders. The game proceeded until there was a winning faction according to the goals described above.

From these experiments, we collected a dataset consisting of both mafia and bystander utterances over the course of each game, as well as the participants' voting behavior.

# Dataset Description

The data is organized as follows:

  Root Dir/
    -Experiment Dir1/
      -node.csv
      -info.csv
      -network.csv
    -Experiment Dir2/
      -node.csv
      -info.csv
      -network.csv
  …
    -Experiment Dir44/
      -node.csv
      -info.csv
      -network.csv
    -README.docx

Every node.csv file contains the following relevant information for each node in the Mafia network used for the given experiment:

1.	id: a unique node id (note that id “1” corresponds to the source node of the network, for which several of the below columns are not applicable; all other nodes correspond to a player in the game)
2.	creation_time: the time at which the node was created
3.	property1: the fake name that was assigned to the given node, if applicable
4.	property2: a Boolean denoting whether the given node remained alive (ie. had not been eliminated) by the end of the Mafia game
5.	property3: the time at which the node was eliminated if the previous value was “FALSE”
6.	type: the type of the node, which may be either “source” for the source node, “mafioso” for nodes assigned the mafia role, or “bystander” for nodes assigned the bystander role

Every info.csv file contains the following relevant information for each transmission across the Mafia network used for the given experiment:

1.	id: a unique transmission id
2.	creation_time: the time at which the transmission was created
3.	type: the type of transmission, which may be either “info” for information about the game state, “text” for texts between players, or “vote” for votes for who to eliminate.
4.	origin_id: the id corresponding to the node that produced the transmission
5.	contents: the contents of the transmission, which in the case of an “info” contains the current phase and victim, if applicable, in the case of a “text” contains the fake name corresponding to the node that produced the transmission, followed by a colon, a space, and the contents of the text, and in the case of a “vote” contains the fake name corresponding to the node that produced the transmission, followed by a colon, a space, and the contents of the vote

Every network.csv file contains the following relevant information for the Mafia network used for the given experiment:

1.	creation_time: the time at which the network was created
2.	property2: the winner of the Mafia game, which may be either “mafia” or “bystanders”
3.	property3: the fake name that corresponds to the most recently eliminated node
4.	max_size: the maximum number of nodes in the network (note that this is one more than the number of players, as the source node must also be accounted for)
