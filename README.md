# Arabic-Text-To-Speech
This is the source code repository for the Arabic open-source text-to-speech platform Arabic TTS system written in pure Java SE with NeatBeans 8.0 IDE, so it runs on many platforms. and ready for use The documentation on using Arabic TTS just be sure all libraries exist or download from http://sourceforge.net/projects/freetts/files/ in final this simple project you can make better or use parts on your own code :)


package text.to.speech;

/**
 *
 * @author ِAhmed Karam
 */
import java.io.*;
import com.sun.speech.freetts.*;
import java.util.ArrayList;
import javax.swing.JOptionPane;
public class TextToSpeech extends javax.swing.JFrame {

    String arabicLetters;
    String englishLetters;
    ArrayList<String> englistLettersArray = new ArrayList<>();
    
    // Here Arabic characters and their equivalent of the English letters
   
   
    public TextToSpeech() {
        initComponents();
        setLocationRelativeTo(null);
        this.setResizable(false);
        arabicLetters = "ءاأبتثجحخدذرزسشصضطظعغفقكلمنهويةئه";
        englishLetters = new StringBuilder("aaaywhnmlkkfgaztdssszrzdahgstbaaa").reverse().toString();
    }
    
    // Here is button method do translitration on Arabic words and do Do method
        
        if (txtArea.getText().isEmpty() == false) {
            englistLettersArray.clear();
            String phase = txtArea.getText();
            String[] splited = phase.split("\\s+");
            for (String splited1 : splited) {
                for (int x = 0; x < splited1.length(); x++) {
                    String lett = String.valueOf(splited1.charAt(x));
                    if (arabicLetters.contains(lett)) {
                        int index = arabicLetters.indexOf(lett);
                        String engLet = String.valueOf(englishLetters.charAt(index));
                        englistLettersArray.add(engLet);
                    }
                }
                englistLettersArray.add("");
            }
            String transWord = "";
            for (int x = 0; x < englistLettersArray.size(); x++) {
                String letter = englistLettersArray.get(x).toString();
                if (letter.equals("")) {
                    transWord = transWord + " " + letter;
                } else {
                    transWord = transWord + letter;
                }
            }
            Do(transWord);
        } else {
            JOptionPane.showMessageDialog(this, "Write text first", "Error Message", JOptionPane.ERROR_MESSAGE);
            txtArea.requestFocus();
        }
        
    

    // Here class typr roman letters on the filed and identify sound to read words
    
private void Do(String transWord) {
       
    
        Voice voice;
        VoiceManager vm = VoiceManager.getInstance();
        voice = vm.getVoice(VOICNAME);
        voice.allocate();
        voice.setRate(170);
        voice.setPitch(100);
        try {
             StringBuffer res = new StringBuffer();

        String[] strArr = transWord.split(" ");
        for (String str : strArr) {
            char[] stringArray = str.trim().toCharArray();
            stringArray[0] = Character.toUpperCase(stringArray[0]);
            str = new String(stringArray);

            res.append(str).append(" ");
        }
            txtٍٍٍShow.setText("" + res.toString().trim());
            voice.speak(res.toString());
        } catch (Exception e) {
        }
    
    
    
   
    }

}
