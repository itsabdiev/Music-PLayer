< br >
### Languages and Tools:
[<img align="left" alt="Everest" width="36px" src="https://i.pinimg.com/originals/a0/16/3f/a0163ff61b94b13e0a422d6120a3698e.jpg" />][website]
[<img align="left" alt="Intellij" width="36px" src="https://pbs.twimg.com/profile_images/1206618215767584769/zl48EuhC_400x400.jpg" />][Intellij]
[<img align="left" alt="Java " width="36px" src="https://icon-library.com/images/java-icon-png/java-icon-png-2.jpg" />][Java]
[<img align="left" alt="Scene Builder " width="36px" src="https://gluonhq.com/wp-content/uploads/2015/02/SceneBuilderLogo-300x300@2x.png" />][SceneBuilder]
  <details>
  <summary>:zap: Process</summary>
  
 
<!--START_SECTION:activity-->
1. 🎨 Working on design of mp3 player
2. 🧩 Creating structure of code
3. 💾 Using mp3 libraries
4. 🎧 End of work
5. 😎 Enjoy
<!--END_SECTION:activity-->

</details>

---

* Controller.java
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
* Main.java
```java
package sample;

import javafx.application.Application;
import javafx.fxml.FXMLLoader;
import javafx.scene.Parent;
import javafx.scene.Scene;
import javafx.stage.Stage;




public class Main extends Application {

    @Override
    public void start(Stage primaryStage) throws Exception{
        Parent root = FXMLLoader.load(getClass().getResource("sample.fxml"));
        primaryStage.setTitle("");
        primaryStage.setScene(new Scene(root, 406, 108));
        primaryStage.show();
        primaryStage.setTitle("◢◤");

    }


    public static void main(String[] args) {
        launch(args);
    }
}

```  
* sample.fxml
```java
<?xml version="1.0" encoding="UTF-8"?>

<?import javafx.scene.control.Button?>
<?import javafx.scene.control.Label?>
<?import javafx.scene.control.Slider?>
<?import javafx.scene.layout.AnchorPane?>
<?import javafx.scene.text.Font?>

<AnchorPane fx:id="pane" maxHeight="-Infinity" maxWidth="-Infinity" minHeight="-Infinity" minWidth="-Infinity" prefHeight="108.0" prefWidth="406.0" style="-fx-background-color: #222222;" xmlns="http://javafx.com/javafx/15.0.1" xmlns:fx="http://javafx.com/fxml/1" fx:controller="sample.Controller">
   <children>
      <Button fx:id="playButton" layoutY="54.0" mnemonicParsing="false" onAction="#playMedia" prefHeight="51.0" prefWidth="56.0" text="▶" wrapText="true">
         <font>
            <Font size="24.0" />
         </font>
      </Button>
      <Label fx:id="songLabel" alignment="CENTER" layoutY="-2.0" prefHeight="0.0" prefWidth="406.0" text="𝅙" textFill="#f0dfdf">
         <font>
            <Font size="39.0" />
         </font>
      </Label>
      <Button fx:id="pauseButton" layoutX="56.0" layoutY="54.0" mnemonicParsing="false" onAction="#pauseMedia" prefHeight="51.0" prefWidth="56.0" text="〓">
         <font>
            <Font size="20.0" />
         </font>
      </Button>
      <Button fx:id="resetButton" layoutX="112.0" layoutY="54.0" mnemonicParsing="false" onAction="#resetMedia" prefHeight="51.0" prefWidth="56.0" text="⏏">
         <font>
            <Font size="22.0" />
         </font>
      </Button>
      
      <Button fx:id="PreviousButton" layoutX="168.0" layoutY="54.0" mnemonicParsing="false" onAction="#previousMedia" prefHeight="51.0" prefWidth="56.0" text="►">
         <font>
            <Font size="24.0" />
         </font>
      </Button>
      <Button fx:id="nextButton" layoutX="224.0" layoutY="54.0" mnemonicParsing="false" onAction="#nextMedia" prefHeight="51.0" prefWidth="56.0" text="◄">
         <font>
            <Font size="24.0" />
         </font>https://itsabdiev.github.io/Everest/
      </Button>
      <Slider fx:id="volumeSlider" layoutX="300.0" layoutY="72.0" max="200.0" prefHeight="9.0" prefWidth="81.0" value="100.0" />
   </children>
</AnchorPane>

```

[website]: https://itsabdiev.github.io/Everest/
[Intellij]: https://www.jetbrains.com/
[Java]: https://www.java.com/ru/
[SceneBuilder]: https://gluonhq.com/products/scene-builder/

