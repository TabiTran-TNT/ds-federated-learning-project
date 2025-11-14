# Federated Learning Demo in Python using Socket Programming

This is a repository of the assignment from the course Distributed Learning my friend and I attend. The work is forked a demo project for applying the concepts of federated learning (FL) in Python using socket programming by building and training machine learning (ML) models using FL. The ML model is trained using [PyGAD](https://pygad.readthedocs.io) which trains ML models using the genetic algorithm (GA). The problem used to demonstrate how things work is XOR.

The project builds GUI for the server and the client using [Kivy](https://kivy.org). This has a number of benefits.

- Easy way to manage the client application.
- Ability to make the client available in mobile devices because Kivy supports deploying its desktop apps into mobile apps. As a result, machine learning models could be trained using federated learning by the massive private data available in mobile devices. 

# Project Files

The project has the following files:

- `server.py`: The server Kivy app. It creates a model that is trained on the clients' devices using FL.
- `client1.py`: The client Kivy app which trains the model sent by the server using just 2 samples of the XOR problem.
- `client2.py`: Another client Kivy app that trains the server's model using the other 2 samples in the XOR problem.

# Install PyGAD

Before running the project, the [PyGAD](https://pygad.readthedocs.io/) library must be installed.

```
pip install pygad
```

For Linux and Mac, use `pip3`:

```
pip3 install pygad
```

# Running the Project

Start the project by running the [`server.py`](https://github.com/ahmedfgad/FederatedLearning/blob/master/server.py) file. The GUI of the server Kivy app is shown below. Follow these steps to make sure the server is running and listening for connections.

* Click on the **Create Socket** button to create a socket. 

* Enter the IPv4 address and port number of the server's socket. `localhost` is used if both the server and the clients are running on the same machine. This is just for testing purposes. Practically, they run on different machines. Thus, the user need to specify the IPv4 address (e.g. 192.168.1.4).
* Click on the **Bind Socket** button to bind the create socket to the entered IPv4 address and port number.
* Click on the **Listen to Connections** button to start listening and accepting incoming connections. Each connected device receives the current model to be trained by its local data. Once the model is trained, then no more models will be sent to the connected devices.

![Fig01](https://user-images.githubusercontent.com/16560492/86205885-5af32380-bb6b-11ea-9ca6-149c0170e82b.png)

After running the server, next is to run one or more clients. The project creates 2 clients but you can add more. The only expected change among the different clients is the data being used for training the model sent by the server.

For [`client1.py`](https://github.com/ahmedfgad/FederatedLearning/blob/master/client1.py), here is the training data (2 samples of the XOR problem):

```python
# Preparing the NumPy array of the inputs.
data_inputs = numpy.array([[0, 1],
                           [0, 0]])

# Preparing the NumPy array of the outputs.
data_outputs = numpy.array([1, 
                            0])
```

Here is the training data (other 2 samples of the XOR problem) for the other client ([`client2.py`](https://github.com/ahmedfgad/FederatedLearning/blob/master/client2.py)):

```python
# Preparing the NumPy array of the inputs.
data_inputs = numpy.array([[1, 0],
                           [1, 1]])

# Preparing the NumPy array of the outputs.
data_outputs = numpy.array([1, 
                            0])
```

Just run any client and a GUI will appear like that. You can either run the client at a desktop or a mobile device.

Follow these steps to run the client:

* Click on the **Create Socket** button to create a socket. 

* Enter the IPv4 address and port number of the server's socket. If both the client and the server are running on the same machine, just use `localhost` for the IPv4 address. Otherwise, specify the IPv4 address (e.g. 192.168.1.4).s
* Click on the **Connect to Server** button to create a TCP connection with the server.
* Click on the **Receive & Train Model** button to ask the server to send its current ML model. The model will be trained by the client's local private data. The updated model will be sent back to the server. Once the model is trained, the message **Model is Trained** will appear.

![Fig03](https://user-images.githubusercontent.com/16560492/86206222-292e8c80-bb6c-11ea-9311-1ef4bb467188.jpg)

