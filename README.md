# ML_Programming_Assignment_3
## Back-propagation implementation 
##### Using python
#### There are some functions:
### 1. Handle Data
* LoadDataSet
    1. load iris.data.txt file 
        * Since the class labels are strings, I need to change them in to numbers like [0, 1, 2] to represent the labels
        * return the new-preocessed trainingset
        * After each change, don't forget to clear the list`newdata`, otherwise it will continuously add new items
    
### 2. Initialize network
* init_network 
    1. There are 4 attributes in each examples
        
        * 4 neurons in each hidden layers
        * 2 hidden layers
    2. There are 3 classes of iris.dataset
        * 3 neurons in output layer
        * 1 output layer
    3. Random initial weights in range[-0.1,0.1]

### 3. Forward propagation
* activate
    * Do the inputs-weights multiplication and summation
* transfer
    * Do implement of `sigmoid` activate function
* transfer_derivative
    * Calculate the slope of neuron's output value
* forward_propagate
    * Update neurons in each layers to the last one (output layer)
    

### 4. Back propagation error
* backward_propagate_error
    1.  Use `reverse` to do the calculation from last layer to front one
    2.  Calculate the error of each neuron and its responsibility
        * Formula below:
    ![](https://i.imgur.com/Igj3W17.jpg)
 
    

### **5. Train network** !!! 
* train_network
    1. Do forward propagation
        * Use `forward_propagate`
    2. Do back propagate error calculation to reformat the network
        * Use `backward_propagate_error`
    3. Update the weights by error responsibilities(base on results of `backward_propagate_error`)
        * Use `update_weights`
    4. Do forward propagation **again** in the new weights model
        * Use `forward_propagate`
    5. After finishing all examples(one epoch), calculate MSE by newly(secondly) predicted results
        * Use one hot encoding to transfer [0, 1, 2] classes into [1, 0, 0], [0, 1, 0] and [0, 0, 1] 
        * Do calculation to each outputs (with one-hot-encoding labels)
        ![](https://i.imgur.com/YC6Q5CO.jpg)

    6. Calculate absolute change of MSE and stop when if converge to less than 10^-4
    ![](https://i.imgur.com/dhKp7r6.jpg)

* update_weights
    1. Use results from `backward_propagate_error` to redistribute the weights of each neuron (refer to formula on table 5.2 in figure above, the 5. step)



           
### 6. Main()
* normalize_data
    1. Normalize data first to prevent large attributes from danaging the training
    ![](https://i.imgur.com/67gA6Uc.jpg)

* back_propagate
    1. Set learning rate, hidden layers number and other variables
    2. Packing needed functions and return how many epochs we need to run to converge  'abs fraction of MSE'
    
Problem 1:
* 1. Similar network as probelm 2, only calculates sum of error and accuracy

Result:
![](https://i.imgur.com/KmugUKk.jpg)
![](https://i.imgur.com/RuaewJx.jpg)

Ovserve:
We can see that sum of error do not decrease in first hundreds of epochs, but after a gracefully weihgts modification, the error decreases dramatically to a quite low place.
Similarly, accuracy is a kind of reverse index of sum of error, also dramatically(almost vertical) rises when epoch runs between 300~400.
Therefore, keeping back propagate errors and update weights indeed can make the original-bad model a good one(need some time since I set learning rate 0.1, it "learns slow").


Problem 2:
* 1. With different learning rate [0.1, 0.2, 0.3, 0.4, 0.5]

Result:
* learning rate 0.1
![](https://i.imgur.com/AgLrcoE.jpg)

Observe:
We can see that the MSE is a slowly increasing index in first several epochs, but the absolute fraction of change of MSE is decreasing.


MSE will finally decrease if I don't break the foor loop.


![](https://i.imgur.com/eHoPt3F.jpg)

As learning rate increases, MSE slightly inceases but absolute fraction of change of MSE decreases much more. So we can see a negative slope curve of number-of-epoch-need when learning rate gets higher.

![](https://i.imgur.com/mLhrJpS.jpg)





