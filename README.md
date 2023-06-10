# Computer_Architecture_Simulated-Java

Thought Projects and Patterns:
     The project document has been read and discussed. Major parts are underlined and notes are taken. Problem had been understood. 
Given physical parts (which are “CPU”,“RAM”, “ETHERNET”, “TOKEN-RING”) had been called as “Computer Parts” . Individual classes are created for every part. Consensus was made to keep the code clean. Which is what brings the project team to first application: Façade Pattern.

1.1 Façade Pattern
    In order to keep the code neat and finesse, and provide a unified interface; Façade Pattern had been applied while beginning. A class named “Computer” had been constructed for the role “Façade” in the related pattern. All the “Computer parts” mentioned above are appointed as “Subsystem Classes”.
    By doing so, Least Knowledge Design Principle is achieved since “the Client” using “the Main Class” does not have to know the parts of a Computer.

1.2 Adapter Pattern
    Secondly, on the project description, attention was drawn to the highlighted words. In these words, different data types as return types and parameters were eye-catching. That circumstance eventually arose the require for a spacer in between. Three Adapter Pattern examples are created for this role and structured for object composition. Roles are appointed as follows: Adapters are ethernet adapter, token-ring adapter, ram adapter; Adaptees are ethernet card, token-ring, ram; Targets are Communication Cards for EthernetAdapter and TokenAdapter, Memory Card for Ram adapter.The Client role of CPU was leading to the next question. “Who will use these functions and how?”.

1.3 Command Pattern
    The Command pattern has been implemented to facilitate the storage and execution of commands by CPUs. To adhere to this pattern, Command Interface is defined in the class  “Command”. Concrete Commands had been created to handle specific operations related to MemoryCard (RAM) and CommunicationCard (ETHERNET and TOKEN-RING). The ReadMemoryCommand class is responsible for RAM operations and the RAM operations are utilized by the RamAdapter, whereas the ReadCardCommand class handles operations related to ETHERNET and TOKEN-RING and those classes operations are handled by the TokenAdapter and EthernetAdapter. Additionally, WriteMemoryCommand and WriteCardCommand classes are implemented, which serve the same purpose as their respective Read commands but are designed for writing data using the defined methods in the RAM, ETHERNET, or TOKEN-RING components. The Computer class acts as the Client in our project as it creates Concrete Command Objects and sets their respective Receivers. The CPUs serve as the Invoker, responsible for executing the commands, while the RAM, ETHERNET, and TOKEN-RING components act as the Receivers, performing the actual work as requested.
    By utilizing the Command pattern, our project achieves a separation of concerns, allowing for more flexibility and extensibility in handling different types of commands and their execution within the system. Command pattern provides the ease of queueing commands as well.


1.4 Template Method Pattern
    Every thread that would carry out a task was assigned a specified order in the project description. This led to the belief that the Template Pattern would be appropriate and useful for the project because the same template could be utilized every time a new task was performed by a new thread, resulting in successful code usage. The Abstract Class in the template pattern is the "Processing Unit" class, while the Concrete Class is the "CPU".

1.5 Observer Pattern
    Finally, The observer pattern is used to implement a logging system for capturing and recording system events. The SystemEventLog logs the completed tasks in its event log, providing a centralized record of system events. Other parts of the system can also observe and react to the completion of tasks by registering additional observers that implement the EventLogObserver interface. Moving onto the roles. The Project’s Abstract Subject is the “Processing Unit” class and Concrete Subject is the “CPU” class.  Abstract Observer is the “Event Log Observer” class and Concrete Observer is the “System Even Log” class. In this implementation, the observer pattern in the Project allows the CPU (subject) to notify the SystemEventLog (observer) whenever a task is completed.

   This is how this project is thought with the task creation, execution, and notification process lined up.







Code Explanation

Classes
1. Adapters
    1.1 MemoryCard
        1.1.1RamAdapter
    1.2 Communication Card
        1.2.1 EthernetAdapter
        1.2.2 TokenAdapter
   
2.Commands
    2.1 Command:
        2.1.1 ReadCardCommand
        2.1.2 ReadMemoryCommand
        2.1.3 WriteCardCommand
        2.1.4 WriteMemoryCommand
      
3. Observer_and_Template
    3.1ProcessingUnit
    3.2 EventLogObserver
        3.2.1 SystemEventLog

4. Main
    4.1 Main:
    4.2 Computer
    4.3 ETHERNET
    4.4 TOKEN_RING
    4.5 RAM





















Contents of the Classes
1. Adapters
    1.1 MemoryCard:
Description:
A memory card is represented by the MemoryCard interface. The processes for reading and writing data to the memory card are described.

Key Methods:
getMem(int addr, int size)
Description: Retrieves data from the memory card.
Return Type: byte[]
Parameters:
addr (int): The beginning  address from where to retrieve the data.
size (int): The size of the data in process.
Usage:   Using the supplied address (addr) and size (size), this function obtains data from the memory card. The data is returned as a byte array (byte[]).

setMem(byte[] data, int addr)
Description: Writes data to the memory card.
Return Type: int
Parameters:
data (byte[]): the data that will be stored on the memory card.
addr: the beginning address at which data should be written (int).
Usage: This method begins writing the provided data (data) to the memory card at the address (addr) that is specified. The amount of bytes written is returned as proof of success.

        1.1.1RamAdapter:
Description:
The RamAdapter class is an implementation of the MemoryCard interface that adapts the RAM class to provide memory operations.

Key Methods:
RamAdapter(RAM ram)
Description: Constructor for the RamAdapter class.
Parameters:
ram (RAM): An instance of the RAM class to be used for memory operations.
Usage: Initializes the ram attribute with the provided RAM object.
getMem(int addr, int size)
Description: Retrieves data from the memory.
Return Type: byte[]
Parameters:
addr (int): The address to start retrieving data from.
size (int): The amount of data to be retrieved in bytes.

Usage: gives control of memory retrieval to the underlying RAM object's get() method. The data that was retrieved is returned after passing the address and size parameters to the get() function.

setMem(byte[] data, int addr)
Description: Writes data to the memory.
Return Type: int
Parameters:
data (byte[]): The data to be written to the memory.
addr (int): The starting address where the data should be written.
Usage: Delegates the memory writing operation to the underlying RAM object's set() method. It sends the data and address parameters to the set() method, which writes the data and then returns the next available address.


    1.2 Communication Card:
Description:
A contract for communication card adapters is represented by the CommunicationCard interface. It is intended to be used with a variety of communication devices, including EthernetAdapter and TokenAdapter. The interface was created with the Open-Closed Principle (OCP) in mind, making it simple to add support for additional communication card kinds in the code.

Key Methods:
getCom(int size):
Description: This method retrieves communication data from the card.
Return Type: byte[]
Parameters:
size (int): The desired size of the communication data to retrieve.
Usage:Usage: Implementing classes should offer this method's implementation to extract communication data from a card of a specific type. The size option specifies the size of the data that has to be retrieved.
setCom(byte[] data):
Description: This method sets communication data on the card.
Return Type: int
Parameters:
data (byte[]): The communication data to be set on the card.
Usage: Classes that implement this method should offer an implementation for setting communication data on a particular type of card. The communication data that must be set is represented by the data parameter.

        1.2.1 EthernetAdapter:

Description:
The EthernetAdapter class acts as an adapter for the Ethernet communication card by implementing the CommunicationCard interface. Through the conversion of data types between byte arrays (byte[]) and Byte arrays (Byte[]), it enables connection with the Ethernet card.

Key Methods:
EthernetAdapter(ETHERNET communicationCard):
Description: Constructor method for the EthernetAdapter class.
Parameters:
communicationCard (ETHERNET): The underlying ETHERNET communication card to be adapted.
Usage: This constructor initializes the EthernetAdapter with the provided ETHERNET communication card.
getCom(int size):
escription: Retrieves data from the Ethernet communication card.
Return Type: byte[]
Parameters:
size (int): The desired size of the data to retrieve.
Usage:By invoking the read() method of the underlying ETHERNET communication card, this method reads data from it. The data is then changed from byte[] to Byte[] and returned.
setCom(byte[] data):
Description: Writes data to the Ethernet communication card.
Return Type: int
Parameters:
data (byte[]): The data to be written to the Ethernet card.
UsageBy transforming the byte[] data to Byte[], this technique writes data to the underlying ETHERNET communication card. The ETHERNET communication card's write() method is then invoked, and the outcome is returned.

        1.2.2 TokenAdapter:
Description:

The TOKEN_RING communication card is modified to work with the interface methods by the TokenAdapter class, which implements the CommunicationCard interface.

Key Methods:
getCom(int size):
Description: the TOKEN_RING card is used to retrieve communication information.
Parameters:
size (int): The size of the data to be retrieved.
Return Type: byte[]
Usage: Uses the TOKEN_RING card's receive() method to simulate receiving data of the desired size. The received int[] data is converted to bytes[] and then returned.
setCom(byte[] data):
Description: Sets communication data to the TOKEN_RING card.
Parameters:
data (byte[]): The data to be set.
Return Type: int
Usage: Converts the data from bytes to integers. uses the TOKEN_RING card's send() method to simulate sending the transformed data. as a sign of success, returns the size of the data that was transmitted.

   
2.Commands
    2.1 Command: 
Description:
The Command interface represents an abstraction of a command that spells out the terms under which it will be carried out and its name will be returned.

Key Methods:
execute()
Description: This method is responsible for executing the command.
Return Type: void
Parameters: None
Usage: By implementing this method, the concrete classes that implement the Command interface define the specific actions to be performed when the command is executed.
getName()
Description: This method retrieves the name of the command.
Return Type: String
Parameters: None
Usage: Implementing classes should provide an implementation for this method to return the name associated with the command. The name can be used for display purposes or to identify the command uniquely.

        2.1.1 ReadCardCommand:
Description:
The ReadCardCommand class implements the Command interface and represents a command to read data from a communication card.
Key Methods:
ReadCardCommand(CommunicationCard communicationCard, int size)
Description: Constructor for the ReadCardCommand class.
Parameters:
communicationCard (CommunicationCard): The communication card to read data from.
size (int): The size of the data to read.
Usage: Initializes the communicationCard, size, and name attributes with the provided values.
execute()
Description: Executes the read card command.
Return Type: void
Usage: Retrieves data from the communication card by calling the getCom() method of the underlying communication card object. IThe size parameter is passed to the getCom() method, which returns a byte array as a result. The String constructor is then used to turn the byte array into a string, and the outcome is printed to the console.
getName()
Description: Returns the command's name.
Return Type: String
Usage: Returns the value of the name attribute.

        2.1.2 ReadMemoryCommand:Description:
The ReadMemoryCommand class implements the Command interface and represents a command to read data from a memory card.

Key Methods:
ReadMemoryCommand(MemoryCard memoryCard, int address, int size)
Description: Constructor for the ReadMemoryCommand class.
Parameters:
memoryCard (MemoryCard): The memory card to read data from.
address (int): The starting address from where to read the data.
size (int): The size of the data to read.
Usage: Initializes the memoryCard, address, size, and name attributes with the provided values.
execute()
Description: Executes the read memory command.
Return Type: void
Usage: Calls the getMem() function of the underlying memory card object to retrieve data from the memory card. The getMem() method is called, and it returns a byte array after receiving the address and size parameters. The String constructor is then used to turn the byte array into a string, and the outcome is printed to the console.
getName()
Description: Retrieves  the name of the command.
Return Type: String
Usage: Returns the value of the name attribute.

        2.1.3 WriteCardCommand:
Description:
The WriteCardCommand class represents a command to write data to a communication card by implementing the Command interface.

Key Methods:
execute():
Description: calls the communication card's setCom() function to carry out the write command.
Return Type: void
Usage:passes the information to the communicationCard's setCom() method to simulate writing it to the card. prints the write operation's outcome to the console.
getName():
Description: returns the command's name..
Return Type: String
Usage: returns the name attribute's value.

        2.1.4 WriteMemoryCommand:
Description:
The WriteMemoryCommand class represents a command to write data to a memory card and implements the Command interface.

Key Methods:
execute():
Description: Executes the write command by calling the setMem() method of the memory card.
Return Type: void
Usage: Passes the data and address to the setMem() method of the memoryCard to simulate writing the data to the memory card. The operation's outcome is printed to the console.
getName():
Description: Retrieves  the name of the command.
Return Type: String
Usage: Returns the value of the name attribute.

      
3. Observer_and_Template
    3.1ProcessingUnit:
Description:
The abstract class ProcessingUnit acts as the subject in the observer pattern. It offers a standard structure and behavior for many processing unit types. The class keeps track of an event log observer's name, reference, and command queue. It includes abstract methods for adding an event log observer, obtaining, running, and informing observers of commands as well as deleting commands. Along with hooks for extra operations during execution, it also offers a means to execute orders in the queue.

Key Methods:
setEventLogObserver(EventLogObserver observer):
Description: Sets the event log observer for the processing unit.
Return Type: void
Parameters:
observer (EventLogObserver): The event log observer to be set.
Usage: The event log observer for the processing unit is configured using this manner. When tasks are completed, the observer will be informed.
getCommand():
Description: Retrieves the next command from the queue.
Return Type: Command
Usage: This method selects the subsequent command from the command queue. Depending on the particular type of processing unit, this method's implementation could differ.
execute():
Description: Executes the current command.
Return Type: void
Usage: The current command is carried out via this way. The way this strategy is put into practice relies on the type of processing unit in question and how commands are actually executed.
notifyObservers():
Description: Notifies the event log observer about the completion of a command.
Return Type: void
Usage: This method alerts the event log observer when a command has finished. Invoking the appropriate event log observer method and supplying pertinent data about the accomplished job are possible steps in the implementation of this function.
removeCommand():
Description: Removes the current command from the queue.
Return Type: void
Usage: The current command is taken out of the command queue using this method.  This technique's application is dependent on the particular type of processing unit and the command queue management system.
executeCommand():
Description: Executes all commands in the queue.
Return Type: void
Usage: This method is used to carry out each and every command in the command queue.  It carries out a succession of specified tasks, including as taking in commands, processing them, notifying observers, and finally erasing the commands. Additionally, it features hooks (hook1(), hook2(), hook3(), and hook4()) that enable other activities to be carried out while it is being executed.
setTasks(Command... tasks):
Description: Sets the tasks (commands) in the processing unit.
Return Type: void
Parameters:
tasks (Command[]): The tasks (commands) to be set in the processing unit.
Usage:  By adding commands to the command queue, this approach establishes the tasks (commands) in the processing unit.
hook1(), hook2(), hook3(), hook4():
Description: Hooks for additional operations during the execution process.
Return Type: void
Usage: Subclasses can implement extra operations at particular points in the execution process using these abstract methods as hooks. The needs and actions of the subclass determine the precise implementation specifics.


       3.1.1 CPU
Description:The CPU class extends the ProcessingUnit class and represents the central processing unit of a computersystem. It overrides some methods of the parent class and provides additional CPU-specific functionality.

Key Methods:
CPU(String name)
Description: Constructor method for the CPU class.
Parameters:
name (String): The name of the CPU.
Usage: This constructor initializes the CPU by setting its name and creating a new LinkedList to store commands.
getCommand()
Description: Retrieves the next command to be executed.
Return Type: Command
Usage: The next instruction in the CPU's stored instruction queue is returned by this procedure. The LinkedList's peek() function is used to obtain the command.
execute()
Description: Executes the current command.
Return Type: void
Usage: This method executes the current command by calling its execute() method.
removeCommand()
Description: Removes the current command from the queue.
Return Type: void
Usage: This method removes the current command from the queue of commands stored in the CPU by calling the remove() method of the LinkedList.
setTasks(Command… tasks)
Description: Sets tasks to be executed by the CPU.
Return Type: void
Parameters:
tasks (Command...): Variable number of tasks/commands to be set.
Usage: This method adds the given tasks/commands to the queue of commands stored in the CPU using the addAll() method of the Collections class.
setEventLogObserver(EventLogObserver observer)
Description: Sets the event log observer for the CPU.
Return Type: void
Parameters:
observer (EventLogObserver): The event log observer to be set.
Usage: This method sets the event log observer for the CPU, allowing it to notify the observer when a task is completed.
    3.2 EventLogObserver:
Description:
The EventLogObserver is like a person who gets told when something is done. They know how to deal with finished tasks, what their name is, and how to show a list of everything that happened.

Key Methods:
taskCompleted(String taskName, String puName):
Description: Notifies the observer about the completion of a task.
Return Type: void
Parameters:
taskName (String): The name of the completed task.
puName (String): The name of the processing unit associated with the task.
Usage: When a job is finished, this method is called to inform observers. The puName argument gives the name of the processing unit connected to the task, and the taskName parameter specifies the name of the finished task. By using this technique, you may react when a task is finished. 
getObserverName():
Description: Retrieves the name of the observer.
Return Type: String
Usage: This method is called to retrieve the name of the observer. The implementation of this method should return the name of the observer.
printEventLog():
Description: Prints the event log.
Return Type: void
Usage: This method is called to print the event log. Implementing this method should dump the event log to the desired output stream or location. 
        3.2.1 SystemEventLog:
Description:
The SystemEventLog class implements the EventLogObserver interface and represents a system event log that observes and records completed tasks.

Key Methods:
taskCompleted(String taskName, String puName)
Description: Updates the event log with the completed task information.
Parameters:
taskName (String): The name of the completed task.
puName (String): The name of the processing unit that completed the task.
Return Type: void
Usage: Prints a message indicating the completion of the task and the processing unit responsible for it. Appends the task name and the processing unit name together and adds it to the eventLog list.
printEventLog()
Description: Prints the contents of the event log.
Return Type: void
Usage: Prints the heading "The Log is:" followed by each entry in the eventLog list, displaying one entry per line.
getObserverName()
Description: Returns the name of the event log observer.
Return Type: String
Usage: Returns the value of the observerName attribute.

4. Main
    4.1 Main:


Description:
The Main class represents the main entry point of the program where the computer and its components are instantiated, and commands are assigned to the CPUs.

Key Methods:
main(String[] args)
Description: The main programming method, which creates and runs commands and computers..
Return Type: void
Usage: establishes the comp Computer object. creates a dataToWrite byte array from the text "Hello, Ufuk Hocamm!" By constructing WriteCardCommand, ReadCard, and WriteMemoryCommand objects with the proper adapters and data, jobs are assigned to CPU1 and CPU2. uses the Computer class's setTasksToCPU() function to assign tasks to each CPU. calls the startComputer() and shutdownComputer() methods to start and stop the computer, respectively.

    4.2 Computer:
Description:
A computer system made up of processing units, memory cards, communication adapters, and an event log observer is represented by the Computer class. It offers ways to interact with the computer system, such as starting and shutting down the computer, allocating work to different processing units.

Key Methods:
setTasksToCPU(ProcessingUnit pu, Command... commands):
Description: This method sets tasks to a specific processing unit.
Return Type: void
Parameters:
pu (ProcessingUnit): The computer processing unit that will be given work
commands (Command...): The quantity of orders that will be given to the processing unit will vary.
Usage: This method calls the setTasks() function of the processing unit (pu) to allocate the given commands to the selected processing unit (pu).
startComputer():
Description: This method starts the computer system.
Return Type: void
Usage: Using this method, the computer system is started, the commands are run on CPUs 1 and 2, and a success message is displayed to show that the machine has started successfully.
shutdownComputer():
Description: This method shuts down the computer system.
Return Type: void
Usage:Using this method, the computer system is started, the commands are run on CPUs 1 and 2, and a success message is displayed to show that the program has started successfully.
getCpu1()
Description: This method retrieves the CPU1 processing unit.
Return Type: ProcessingUnit
Usage: The instance of the CPU1 processing unit is returned by this method.
getCpu2()
Description: This method retrieves the CPU2 processing unit.
Return Type: ProcessingUnit
Usage: TThe instance of the CPU2  processing unit is returned by this method
getMemoryCard()
Description: This method retrieves the memory card.
Return Type: MemoryCard
Usage: This method returns the instance of the memory card.
getEthernetAdapter()
Description: This method retrieves the Ethernet communication adapter.
Return Type: CommunicationCard
Usage: The instance of the Ethernet communication adapter is returned by this method.
getTokenAdapter()
Description: This method retrieves the Token communication adapter.
Return Type: CommunicationCard
Usage: The instance of the Token communication adapter is returned by this method.

    4.3 ETHERNET:
Description:
The ETHERNET class represents an Ethernet communication card. It provides methods for reading and writing data to the Ethernet card.

Key Methods:
read(int size):
Description: Reads data from the Ethernet card.
Return Type: Byte[]
Parameters:
size (int): The desired size of the data to read.
Usage: With this method, the process of reading data from the Ethernet card is simulated. It seeks for a dataset with the required size in the dataList. A matched dataset is removed from the dataList and returned as the outcome if one is discovered. Null is returned if no matching dataset could be located.
write(Byte[] data):
Description: Writes data to the Ethernet card.
Return Type: int
Parameters:
data (Byte[]): The data to be written to the Ethernet card.
Usage: Using this method, writing data to the Ethernet card is simulated. The data to be written is represented by the data parameter. The method returns the length of the data as a sign that it was successful after adding the data to the dataList.

    4.4 TOKEN_RING:
Description:
The token ring communication card is represented by the TOKEN_RING class. It offers ways for data to be sent and received via the card.

Key Methods:
receive(int size):
Description: Simulates receiving data from the TOKEN-RING card.
Parameters:
size (int): The size of the data to be received.
Return Type: int[]
Usage: finds a data set with the required quantity of data by searching the dataList. Removes the data set from the list and returns it as an array if it is found. returns null if no matching data set is discovered.
send(int[] data, int size):
Description: Simulates sending data to the TOKEN-RING card.
Parameters:
data (int[]): The data to be sent.
size (int): The size of the data to be sent.
Return Type: int
Usage: copy the contents of the data array into an array called sendData, which is created with the provided size. sendData array is added to the dataList. As a sign of success, returns the length of the sendData array.
    4.5 RAM:
Description:
The random-access memory module is represented by the RAM class. It offers strategies for getting stuff out of the memory and putting it there.
Key Methods:
get(int addr, int size)
Description: Retrieves data from the memory.
Return Type: byte[]
Parameters:
addr (int): The address to start retrieving data from.
size (int): The amount of data to be retrieved in bytes.
Usage: Using this technique, data starting at the specified address (addr) and of required size are retrieved from the memory. 


set(byte[] data, int addr):
Description: Writes data to the memory.
Return Type: int
Parameters:
data (byte[]): The data to be written to the memory.
addr (int): The starting address where the data should be written.
Usage: The method starts writing the provided data (data) to memory at the designated location (addr). An exception is raised if the address falls outside of the permitted range. As it iterates through the data array, the method copies the entries from the data array into the memory array according to the address given.
