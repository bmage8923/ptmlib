# PTMLib - **P**endragon **T**iny **M**L **Lib**rary

## Summary

**PTMLib** is a set of utilites that I have used while working with Machine Learning frameworks such as Scikit-Learn and TensorFlow.  The purpose is to eliminate code that I kept repeating in multiple Jupyter Notebooks.  

- **ptmlib.time.Stopwatch** - measure the time it takes to complete a long-running task, with an audio alert for task completion
- **ptmlib.cpu.CpuCount** - get info on CPUs available, with options to adjust/exclude based on a specific number/percentage.  Useful for setting `n_jobs` in Scikit-Learn tools that support multiple CPUs, such as `RandomForestClassifier`
- **ptmlib.charts** - render separate line charts for TensorFlow accuracy and loss,with corresponding validation data if available

---

## ptmlib.time: Stopwatch

The `Stopwatch` class is used to measure the amount of time it takes to complete a long-running task.  

When `stop` is called, an audio prompt will alert you that the task has completed. This is can be useful when you are multi-tasking while your code is executing, which is especially helpful if you are time constrained, for example when taking the [TensorFlow Developer Certificate](https://www.tensorflow.org/certificate) exam.

### Example:

```
stopwatch = Stopwatch()

...

stopwatch.start()

history = model.fit(
    training_images,
    training_labels,
    validation_split=hp_validation_split,
    epochs=hp_epochs,
    callbacks=[early_callback]
)

stopwatch.stop()
```

### Output:

```
Start Time: Thu Jan 28 16:57:32 2021
Epoch 1/50
1500/1500 [==============================] - 2s 1ms/step - loss: 0.5316 - accuracy: 0.8086 - val_loss: 0.4141 - val_accuracy: 0.8503

...

1500/1500 [==============================] - 2s 1ms/step - loss: 0.2337 - accuracy: 0.9101 - val_loss: 0.3212 - val_accuracy: 0.8879
End Time:   Thu Jan 28 16:58:03 2021
Elapsed seconds: 30.8191 (0.51 minutes)
```

Start Time, End Time and Elapsed Seconds/Minutes are all output when `start` and `stop` methods are called.  All other information in the above example output would be generated based on your ML framework.  

Stopwatch has been tested using Scikit-Learn and TensorFlow, but can be used for any long-running Python code for which you want to measure performance or be notified of task completion.

Stopwatch has been tested on Windows (including IDEs and Jupyter Notebook) and Google Colab environments.