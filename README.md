# Sample code with examples to simplify connection to Cobolt Lasers
[![Build Status](https://travis-ci.com/cobolt-lasers/samples.svg?branch=master)](https://travis-ci.com/cobolt-lasers/samples)*(Linux and OS X)* ]

This is a cross-platform library for interfacing with rs-232 serial like ports written in C++. It provides a modern C++ interface with a workflow designed to look and feel like PySerial, but with the speed and control provided by C++. 

This library is in use in several robotics related projects and can be built and installed to the OS like most unix libraries with make and then sudo make install, but because it is a catkin project it can also be built along side other catkin projects in a catkin workspace.

Serial is a class that provides the basic interface common to serial libraries (open, close, read, write, etc..) and requires no extra dependencies. It also provides tight control over timeouts and control over handshaking lines. 
