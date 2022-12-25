# Distributed_system_coursework
Understanding sockets 
BSE 3202 – Distributed Systems Development

Project 1: A sequencer-based multicast protocol using Java RMI

Introduction

This project reinforces the material in Section 12.4.3 on how to achieve total ordering with a sequencer. It also gives students experience in the use of the Java API to IP multicast (Section 4.5.1).

What is required

Your task is to create a sequencer-based multicasting service, using a slight variant of the simple version of the Amoeba protocol (the first protocol described in www.cdk3.net/coordination), and a small client application to exercise it. You will use Java RMI and multicast sockets.

The main classes in your implementation will be:





 

TestSequencer.java – each instance (you will create several) will allow the user to enter strings and multicast them to a group of instances of TestSequencer. TestSequencer will also be capable of “stress-testing” – multicasting messages as fast as possible.

Group.java – TestSequencer uses an instance of Group for group communication services. Group in turn uses a MulticastSocket to receive incoming messages, and uses RMI to the sequencer for sending messages and other, sequencer-specific operations Sequencer.java, SequencerImpl.java – the interface to and implementation of a sequencer. History.java – the implementation of the sequencer's history. History does not need to have a fixed capacity, but obsolete items should be removed whenever its size grows beyond a threshold, say 1024 entries.

Attached you will find (i) the RMI interface to an object which will implement the sequencer (Sequencer.java), (ii) two trivial classes associated with the Sequencer definition (SequencerJoinInfo.java and SequencerException.java), (iii) outline code for Group.java, and (iv) some hints on marchalling messages into datagram packets.

You need to write SequencerImpl.java and History.java from scratch.

Note that the scheme you produce will not precisely implement the Amoeba protocol. In that protocol, messages are sent unreliably to the sequencer in the first instance. In yours, messages to be multicast are handed to the sequencer using RMI.

Choosing a multicast address and time-to-live

SequencerImpl should take as an argument the IP multicast address that the corresponding Groups are to use. To avoid collisions with numbers chosen by others, incorporate a random number into the multicast IP address that you use – e.g. 234.day.month.rand where rand is a random number between 1 and 254.

Don't set your sockets' time-to-live (TTL) to more than 1. That way, your multicast packets will not be transmitted beyond the local router.

Organization

This project is suitable for implementation by groups of four or six students. The following division of labor might be used: 1. Team members 1 & 2: SequencerImpl.java and any associated helper classes apart from History

2. Team members 3 & 4: Group.java

3. Team members 5 & 6: TestSequencer.java and History.java

Teams hand in all written code. Teams are required to demonstrate their implementation. The demonstration should include as many as possible of the following features: simple message sending, stress-testing, recovery from simulated multicast datagram loss, heartbeat messages and history truncation.

Hints: Marshalling data into a datagram

ByteArrayOutputStream bstream = new ByteArrayOutputStream(MAX_MSG_LENGTH); DataOutputStream dstream = new DataOutputStream(bstream); dstream.writeLong(aLong); // marshals a Long into the byte array underlying bstream // …

// After marshalling, the data can be obtained from bstream for inclusion in a DatagramPacket:

byte[] theData = bstream.toByteArray(); (For unmarshalling there are corresponding classes ByteArrayInputStream and DataInputStream.)

This assignment is due 4 weeks from the 22 nd of June, 2022.

