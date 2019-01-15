import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.scene.Scene;
import javafx.scene.text.Font;
import javafx.scene.control.Button;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;
import javafx.stage.WindowEvent;
import javafx.scene.control.Label;
import javafx.geometry.Insets;
import javafx.scene.control.TextField;
import java.util.ArrayList;
import java.io.*;
import javafx.application.Platform;
import javafx.geometry.HPos;
import java.util.Random;


public class French extends Application 
{
   Button button;
   
   public static void main( String[] args )
   {
      launch( args );
      Platform.setImplicitExit(true);
      Platform.exit();
   }
   
   public void start( Stage primaryStage ) throws Exception
   {
      
      ArrayList< String > english = new ArrayList< String >();
      ArrayList< String > french = new ArrayList< String >();
      
      ArrayList< Integer > hash = new ArrayList< Integer >();
      
      try
      {
         FileReader fr = new FileReader( "words.txt" );
         BufferedReader br = new BufferedReader( fr );
        
         
         String line = br.readLine();
         
         while( line != null )
         {
            english.add( line );
            line = br.readLine();
            french.add( line );
            line = br.readLine();
         }
         
         br.close();
         fr.close();
      }
      catch( Exception e ){};
      
      Random ran = new Random();
      
      for( int i = 0; i < english.size(); i++ )
      {
         int x = ran.nextInt( english.size() );
                
         while( Inside( x,hash ) )
         {
            x = ran.nextInt( english.size() );
         }
         
         hash.add( x );  
      }
       
      
      Stage window = primaryStage;
      
      window.setOnCloseRequest( new EventHandler< WindowEvent>()
      {
         public void handle( WindowEvent e )
         {
            Platform.exit();
            System.exit( 0 );
            Platform.setImplicitExit(true);
         }
      });
      
      window.setTitle( "Language test" );


      Label label = new Label( english.get( hash.get( 0 ) ) );
      TextField field = new TextField();
      label.setFont( new Font( "Times New Roman",55 ) );
      Button button = new Button( "Check" );
      
      Label counter = new Label( 1 + "/" + english.size() );
      counter.setFont( new Font( "Times New Roman",20 ) );
      
      Label mistakes = new Label( "Wrong: " + 0 );
      mistakes.setFont( new Font( "Times New Roman",20 ) );
      
      
      button.setStyle("-fx-font-size: 25pt;");
      field.setPrefWidth( 500 );
      
      button.setOnAction( new EventHandler<ActionEvent>() 
      {
         int mistakesI = 0;
         public void handle( ActionEvent e ) 
         {           
            String answer = field.getText();

            if( !hash.isEmpty() )
            {           
               if( !answer.toLowerCase().equals( french.get( hash.get( 0 ) ) ) )
               {
                  answer = field.getText();
                  mistakes.setText( "Wrong: " + ++mistakesI );
               }
               else
               {
                  hash.remove( 0 );
                  field.clear();
                  
                  if( !hash.isEmpty() )
                  {
                     label.setText( english.get( hash.get( 0 ) ) );
                     counter.setText( ( english.size() - hash.size() + 1 ) + "/" + english.size() );
                  }
                  else
                  {
                     label.setText( "FIN" );
                     return;
                  }
               }
            }              
         }
      });


      GridPane grid = new GridPane();
      
      grid.setVgap( 40 );
      grid.setHgap( 50 );
      
      GridPane.setHalignment( label, HPos.CENTER );
      GridPane.setHalignment( field, HPos.CENTER );
      GridPane.setHalignment( button, HPos.CENTER );
      GridPane.setHalignment( counter, HPos.LEFT );
      GridPane.setHalignment( mistakes, HPos.LEFT );
      
      GridPane.setConstraints( label,2,2 );
      GridPane.setConstraints( field,2,4 );
      GridPane.setConstraints( button,2,6 );
      GridPane.setConstraints( counter,1,8 );
      GridPane.setConstraints( mistakes,1,9 );
      
      grid.getChildren().addAll( label,field,button,counter,mistakes );
      

      Scene scene = new Scene( grid,860,600 );
      window.setScene( scene );
      window.show();
      
   }
   
   public static boolean Inside( int x,ArrayList hash )
   {
      boolean result = false;
      
      for( int j = 0; j < hash.size(); j++ )
      {
         if( x == (int)hash.get( j ) )
         {
            result = true;
            break;
         }
      }
      
      return result;
   } 
}
