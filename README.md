
```java
package sample;

import javafx.beans.value.ChangeListener;
import javafx.beans.value.ObservableValue;
import javafx.scene.media.Media;
import javafx.scene.media.MediaPlayer;

import javafx.fxml.FXML;
import javafx.fxml.Initializable;

import javafx.scene.control.*;


import javafx.util.Duration;

import java.io.File;
import java.net.URL;

import java.util.*;

public class Controller implements Initializable {


    @FXML
    private Label songlabel;
    @FXML
    private Button playButton,pauseButton,resetButton,previousButton,nextButton;
    @FXML
    private ComboBox<String> speedbox;
    @FXML
    private Slider volumeSlider;
    @FXML
    private ProgressBar songProgressBar;
    private Media media;
    private MediaPlayer mediaPlayer;

    private File directory;
    private File[] files;
    private ArrayList<File> songs;
    private int songNumber;
    @Override
    public void initialize(URL url, ResourceBundle resourceBundle) {
        songs = new ArrayList<File>();
        directory = new File("music");
        files = directory.listFiles();
        if (files != null) {
            for (File file : files) {
                songs.add(file);

            }

        }
        media =  new Media(songs.get(songNumber).toURI().toString());
        mediaPlayer = new MediaPlayer(media);
        volumeSlider.valueProperty().addListener(new ChangeListener<Number>() {
            @Override
            public void changed(ObservableValue<? extends Number> observableValue, Number number, Number t1) {
                mediaPlayer.setVolume(volumeSlider.getValue() * 0.01);
            }
        });
    }
    public void playMedia() {
        mediaPlayer.play();
    }
    public void pauseMedia() {
        mediaPlayer.stop();

    }
    public void resetMedia() {
        mediaPlayer.seek(Duration.seconds(0));
    }
    public void previousMedia() {
        if(songNumber > 0) {
            songNumber--;
            mediaPlayer.stop();

            media =  new Media(songs.get(songNumber).toURI().toString());
            mediaPlayer = new MediaPlayer(media);
            mediaPlayer.play();

        }else {
            songNumber = songs.size() -  1;
            mediaPlayer.stop();

            media =  new Media(songs.get(songNumber).toURI().toString());
            mediaPlayer = new MediaPlayer(media);
            mediaPlayer.play();
        }
    }
    public void nextMedia() {
        if(songNumber < songs.size() - 1) {
            songNumber++;

        }else {
            songNumber = 0;

        }
        mediaPlayer.stop();
        media =  new Media(songs.get(songNumber).toURI().toString());
        mediaPlayer = new MediaPlayer(media);
        mediaPlayer.play();
    }

}
```
