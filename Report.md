For this assignment I mainly used code by the original author, which I altered at some points based on my needs. These points are mentioned later in the report.

**Part 1**

The model performed inconsistently on the dataset, giving me different kinds of accuracies (significantly lower than in the original blog, i.e. 23%, 49%, and 52% at times), no matter the amount of data I used each time. It was worse every time I run it. Judging by the results on the blog, the model should be able to predict text characters from images with high confidence.The Character Accuracy shows that it is able to succesfully identify individual characters, while the Word Accuracy suggests that it can also recognize with ease entire words. 

In order to better examine my low scores, I experimented with different sizes of data, using 20.000 images for training as the authors or more, in the false hopes of improving my accuracy. However, I still have no clue why this happened and I find it quite odd. I understand that the data can have certain differences, but is that so significant in altering the accuracy scores?

**Part 2**

For this part I altered the existing dataset class to suit my approach in dealing with this assignment. I first created a table with all the image paths and their annotations in order to split them more easily into training and testing later. Then I altered the dataset class to extract all the necessary information from a csv file instead of directory or file paths. Moreover, in order to work with the existing collate function class, I added a resizing tranformation in the dataset class, so all the images would have the same size from the beginning. All the code for the rest of the tasks is in the same python notebook 'part2.ipynb.'

**Parts 4 & 5**

The model seems to not be that smart in predicting the car licence plate number and text, since it gives back very low accuracy scores. Initially, the score was 0%, which improved to 2% by reducing the batch size, suggesting that the model is strugglilng with this task.
 By printing out the predictions and actual labels, I observed that sometimes the model predicts the same character sequence repetitively, no matter the car plate image. This could be due to the limited size of the dataset, which consists of only 167 training instances, devided to train and validation datasets. Hence, the model learns specific patterns that lead to repetitive predictions. I also wrote a function to calculate precision and recall, but they both returned 0% accuracy, which makes sense since the word accuracy is 0 as well.
 Some suggestions to improve the model would be the following strategies:
    Augment the data by transforming the images, i.e., rotate them, adjust the contrast or saturation, etc. Ideally more data would become more diverse and introduce more variability to the training dataset. The model would be expected to be more efficient by this and less likely to make repetitive predictions. The same would happen by expanding the same dataset by collecting more labeled car plate images.

    Moreover, some things I tried to improve the accuracy were reducing the batch size, the learning rate, and exploring new architectures. When we are working with small data, having small batch sizes helps the model learn better, while keeping the learning rate low helps the model generalize. The batch size proved to be helpful in training the model, while the lower learning rate didn't have a significant effect. 

    New architectures I tried included adding more layers to the cnn, adding dropout, changing the max pooling to average pooling, and swapping out the LSTM network for a GRU one.

***adding layers*** : adding more layers (2-3) was expected to make the model fit the training data better, by learning more complex patterns and better representations. In OCR I thought that this would be beneficial, since the early layers would capture image information, while the deeper layers would capture more abstractions and complex features like numbers and text. However, this did not have the results I expected and I did not get higher accuracy scores.

***adding dropout***: the dropout was added as a regularization technique to make the model generalize better, since it is more effective when the amount of training data is small, like in this case. Dropout is used in order to prevent the model from overfitting the data, which was obviously not the case here, but adding it gave a small improvement some times. Still the results were inconsistent. 

***average pooling***: averaging pooling is another technique used when working with small data. It can retain more information about the spatial distribution of features, which sounded beneficial for an OCR task where this kind of information is important. However, the change did not make any significant improvements.

***GUR***: swapping the LSTM for a GRU network made the most significant improvement. GRU is a simpler model with fewer parameters, and can prove to be morebeneficial when we are dealing with few data. It also reduces training times and requires less memory. It seemed fitting for the task at hand because long distance dependecies were not the primary concern, and because it performs well for sequence-to-sequence tasks like OCR. This change yielded better accuracy results.