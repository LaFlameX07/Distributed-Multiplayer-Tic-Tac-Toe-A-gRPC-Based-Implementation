# Distributed Multiplayer Tic-Tac-Toe using gRPC

## Overview

This project implements a distributed multiplayer Tic-Tac-Toe game using gRPC, a high-performance RPC framework. The system follows a client-server architecture where players interact through a command-line interface, and the server manages game logic, state, and synchronization using gRPC for communication. Protocol Buffers (.proto) define the data structures and service methods, ensuring efficient and type-safe communication between clients and the server.

The project demonstrates key distributed systems concepts, including:

* Client-server communication using gRPC over HTTP/2.

* Stateful game session management.

* Synchronous and asynchronous communication for game setup and real-time gameplay.

* Concurrent request handling for multiple players.

* At-least-once and at-most-once call semantics for reliable interactions.

## Features

* Multiplayer Support: Two players can join a game session, taking turns as X or O.

* Real-Time Gameplay: The server synchronizes game state across clients using gRPC.

* Command-Line Interface: Simple and intuitive CLI for creating/joining games and making moves.

* Error Handling: Robust validation for invalid moves, occupied cells, and game state errors.

* Scalable Design: The server supports concurrent game sessions using multithreading.

## Prerequisites
To run this project on your system, ensure you have the following installed:

* Python 3.8+: The project is built using Python.

* pip: Python package manager for installing dependencies.

* gRPC Tools: For compiling Protocol Buffers and generating gRPC code.

* Operating System: Compatible with Windows, macOS, or Linux.

## Installation
Follow these steps to set up the project on your system:

* ### Clone the Repository:

git clone &lt;repository-url&gt;

cd tic-tac-toe-grpc


* ### Set Up a Virtual Environment (recommended):
python -m venv venv

source venv/bin/activate  

On Windows: venv\Scripts\activate


* ### Install Dependencies:Install the required Python packages using pip:
pip install grpcio grpcio-tools


* ### Generate gRPC Code:
The project includes a tic_tac_toe.proto file that defines the service and message structures. 

Compile it to generate the necessary Python code:

python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. tic_tac_toe.proto

This generates tic_tac_toe_pb2.py and tic_tac_toe_pb2_grpc.py in the project directory.


## Project Structure

* tic_tac_toe.proto: Protocol Buffers file defining the gRPC service and messages.

* server.py: Implements the gRPC server, handling game logic and state management.

* client.py: Implements the client-side logic for player interaction and game communication.

* tic_tac_toe_pb2.py: Auto-generated file containing message definitions.

* tic_tac_toe_pb2_grpc.py: Auto-generated file containing gRPC service stubs.

## Running the Project

* Start the Server:Run the gRPC server to listen for client connections:

python server.py

* The server will start on localhost:50051 by default. Ensure the port is free.

* Start the Client:Open a new terminal, activate the virtual environment (if used), and run the client:

python client.py

* Follow the prompts to:

Choose an action: 

(1) Create a new game or (2) Connect to an existing game.

Select a player symbol (X or O).

If connecting to a game, enter the game ID provided when the game was created.


Play the Game:

For a multiplayer game, run two client instances in separate terminals.

One player creates a game, and the other joins using the game ID.

Players take turns entering moves (1–9) based on the displayed board.

The game ends when a player wins or the board is full (draw).



## Example Usage

Start the server:

python server.py

Output: Server listening on 0.0.0.0:50051

Start the first client (Player 1):

python client.py


Choose option 1 to create a new game.

Select X as the player symbol.

Note the game ID (e.g., 123456).


Start the second client (Player 2):

python client.py


Choose option 2 to connect to a game.

Enter the game ID (e.g., 123456).

Select O as the player symbol.


Play the game by entering moves (1–9) in the CLI. The board updates after each move, and the game ends with a win or draw.


## Troubleshooting

* Port Conflict: If port 50051 is in use, modify the port variable in server.py and update SERVER_ADDRESS in client.py to match.

* gRPC Errors: Ensure the server is running before starting clients. Check for correct installation of grpcio and grpcio-tools.

* Game Not Found: Verify the game ID when connecting. Ensure the server hasn’t been restarted, as it clears active games.

* Invalid Moves: Moves must be numbers 1–9 and correspond to unoccupied cells.

## Notes

* The server maintains game state in memory, so restarting the server clears all active games.

* The client uses a simple polling mechanism (GetGame) to check for opponent moves. For production, consider using gRPC streaming for real-time updates.

* The project uses insecure gRPC channels. For production, implement SSL/TLS for secure communication.

## Future Improvements

* Add persistent storage (e.g., Redis) for game state to survive server restarts.
  
* Implement bi-directional streaming RPCs for real-time move updates.
  
* Enhance the client with a graphical user interface (GUI) using a framework like Tkinter or PyQt.
  
* Add support for multiple concurrent games with unique session management.

## License
This project is licensed under the MIT License. 

See the [LICENSE](https://grok.com/chat/LICENSE) file for details.
