package cutfile;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.BufferedOutputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.nio.MappedByteBuffer;
import java.nio.channels.FileChannel;

public class CutFile {
   CutFile(String args[]){
    File fileIn;
    int cutSizeMb;MappedByteBuffer mapByteBuff;
    BufferedOutputStream bo;
          try {
      fileIn = new File(args[0]);
      cutSizeMb = Integer.parseInt(args[1]);
      FileChannel fc = new FileInputStream(fileIn).getChannel();
      if (Math.abs(cutSizeMb)*1024*1024 >=fileIn.length()){
       System.out.println(" Cut Size > File Lenth !");
      } else{      
        bo =new BufferedOutputStream(new FileOutputStream(args[2],false));
        if (cutSizeMb>=0) {
         mapByteBuff = fc.map(FileChannel.MapMode.READ_ONLY,0,cutSizeMb*1024*1024 );
        } else {
         mapByteBuff = fc.map(FileChannel.MapMode.READ_ONLY,fileIn.length()-Math.abs(cutSizeMb)*1024*1024,Math.abs(cutSizeMb)*1024*1024);
          }
        byte[] data = new byte[(int)(Math.abs(cutSizeMb)*1024*1024)];
        mapByteBuff.get(data);
        fc.close();
        bo.write(data);
        }
      } catch (FileNotFoundException ex) {
            System.out.println(ex);
        } catch (IOException ex1) {
            System.out.println(ex1);
        }
    }
    public static void main(String args[]){ //filename,int cutSize) {
       CutFile cutFile = new CutFile(args);
    }    
}
