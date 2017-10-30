# Keras-real-time-age-gender-estimation-demo
I use the following code to train the keras model
https://github.com/yu4u/age-gender-estimation

## Small model

TYY_1stream:
```
        inputs = Input(shape=self._input_shape)

        x = Conv2D(32,(3,3),activation='relu')(inputs)
        x = MaxPooling2D(2,2)(x)
        x = Conv2D(32,(3,3),activation='relu')(x)
        x = MaxPooling2D(2,2)(x)
        x = Conv2D(64,(3,3),activation='relu')(x)
        x = MaxPooling2D(2,2)(x)
        x = Conv2D(64,(3,3),activation='relu')(x)
        x = BatchNormalization(axis=self._channel_axis)(x)

        # Classifier block
        pool = AveragePooling2D(pool_size=(4, 4), strides=(1, 1), padding="same")(x)
        flatten = Flatten()(pool)
        predictions_g = Dense(units=2, kernel_initializer=self._weight_init, use_bias=self._use_bias,
                              kernel_regularizer=l2(self._weight_decay), activation="softmax")(flatten)
        predictions_a = Dense(units=21, kernel_initializer=self._weight_init, use_bias=self._use_bias,
                              kernel_regularizer=l2(self._weight_decay), activation="softmax")(flatten)

        model = Model(inputs=inputs, outputs=[predictions_g, predictions_a])
```


## Demo

Change the video name of the code for your demo
```
clip = VideoFileClip('mewtwo.mp4') # can be gif or movie
```

Unlike the demo.py in https://github.com/yu4u/age-gender-estimation
,I made several adjustment for the demo.

***Use [[moviepy]] instead of [[cv2]] for the frame of the video!!!***

There are a lot of issue of using cv2.VideoCapture()
https://github.com/ContinuumIO/anaconda-issues/issues/121

