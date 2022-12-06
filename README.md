# Login-Page-with-encryption-java
Login page with data encryption and decryption of credentials.

******************************************************
v1.0 released, check changelogs file for more details.
******************************************************

This code is solely witten in JAVA by AYUSH and its free to use as long as you don't consider the code as your's.

Details:
This program will show a login page as soon as you run it, and as soon as you enter your credentials and press "Sign Up", it will encrypt your credentials and save it to "C:\Users\username\Documents\Details\Credentials.txt".  ̶N̶o̶t̶e̶ ̶t̶h̶a̶t̶ ̶t̶h̶e̶ ̶e̶n̶c̶r̶y̶p̶t̶i̶o̶n̶ ̶i̶s̶ ̶v̶e̶r̶y̶ ̶b̶a̶s̶i̶c̶ ̶a̶n̶d̶ ̶c̶a̶n̶ ̶b̶e̶ ̶c̶r̶a̶c̶k̶e̶d̶ ̶e̶a̶s̶i̶l̶y̶.̶

Now you can use the same credentials to login (or run the real program) as long as the "Credentials.txt" is not deleted or modified manually. The program will read and decrypt the credentials in the file and compare it to the credentials you entered, if both matches, then it will print "IT'S WORKING!" (You can change the function) and will close the GUI.

Features of the program:
* Can store credentials for future login (Credentials will be encrypted)
* Can add new credentials
* You can use it to create instance of other class and it will work as a login system
* Can change theme of the page (Light and Dark)
* and Many More!

Check some screenshots:
![Screenshot (15)](https://user-images.githubusercontent.com/119154806/204243974-a5772a56-167d-4871-9075-ed42161656a5.png)
![Screenshot (16)](https://user-images.githubusercontent.com/119154806/204244012-9cbbc6f3-8db7-473c-8ac4-4daee71dfd64.png)
![Screenshot (17)](https://user-images.githubusercontent.com/119154806/204244038-ddc4a632-f1cd-4702-86b0-0c406400dc7d.png)

Details (About Code):
* You can change line 157 to do it what you want to as soon as you login (Create instance of another GUI class and it will launch that)
* The code is easy to understand and its under 250 lines of code
* If you need any help regarding the code, contact me on telegram at @SOUL_AYU

Check out the code (v1.0):

	import java.awt.*;
	import java.awt.event.*;
	import java.io.*;
	import javax.swing.*;

	public class LoginPage extends JFrame implements ActionListener{
	
	private static final long serialVersionUID = 1L;
	JLabel lab[] = new JLabel[5];
	JTextField uname;
	JPasswordField pword;
	JButton but[] = new JButton[3];
	String n,p;
	static String alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
	
	//TEXT ENCRYPTION LOGIC
	String encrypt(String plainText, int shiftKey)
    {
       // plainText = plainText.toLowerCase();
        String cipherText = "";
        for (int i = 0; i < plainText.length(); i++)
        {
            int charPosition = alphabet.indexOf(plainText.charAt(i));
            int keyVal = (shiftKey + charPosition) % 52;
            char replaceVal = alphabet.charAt(keyVal);
            cipherText += replaceVal;
        }
        return cipherText;
    }
	
	//TEXT DECRYPTION LOGIC
	   public static String decrypt(String cipherText, int shiftKey)
	    {
	       // cipherText = cipherText.toLowerCase();
	        String plainText = "";
	        for (int i = 0; i < cipherText.length(); i++)
	        {
	            int charPosition = alphabet.indexOf(cipherText.charAt(i));
	            int keyVal = (charPosition - shiftKey) % 52;
	            if (keyVal < 0)
	            {
	                keyVal = alphabet.length() + keyVal;
	            }
	            char replaceVal = alphabet.charAt(keyVal);
	            plainText += replaceVal;
	        }
	        return plainText;
	    }
	
	//STORING CREDENTIALS IN A FILE
	void appendingText() {
		BufferedWriter writer = null;
		try {
			writer = new BufferedWriter(new FileWriter("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt" , true)); 
			writer.append("\n"+encrypt(String.valueOf(uname.getText()), 5));
			writer.append(" : ");
			writer.append(encrypt(String.valueOf(pword.getPassword()), 5));
		    	} catch (Exception e) {}
				finally {
		    		try {
		    			writer.close();
		    		} catch (Exception e) {}
		    	}
	}
	
	LoginPage(){
		//CREATION OF LABELS
		String labels[] = {"LOGIN PAGE","", "Username:", "Password:", "------------------"};
		String buttons[] = {"Login", "Sign Up", "Theme: Light"};
		for(int i=0; i<5; i++) {
			lab[i] = new JLabel(labels[i]);
			lab[i].setFont(new Font("MV Boli", Font.PLAIN, 15));
			lab[i].setForeground(Color.RED);
			lab[i].setVisible(true);
			this.add(lab[i]);
			if(i<3) {
				but[i] = new JButton(buttons[i]);
				but[i].setBackground(new Color(123,100,255));
				but[i].setFont(new Font("MV Boli", Font.PLAIN, 15));
				but[i].setFocusable(false);
				but[i].setVisible(true);
				but[i].addActionListener(this);
				this.add(but[i]);
			}
		}
		
		//SETTING POSITIONS
		lab[0].setBounds(75, -30, 150, 100);
		lab[4].setBounds(75, -18, 150, 100);
		lab[0].setFont(new Font("MV Boli", Font.PLAIN, 20));
		lab[1].setBounds(20, 0, 150, 100);
		lab[1].setFont(new Font("MV Boli", Font.PLAIN, 12));
		lab[2].setBounds(20, 55, 150, 40);
		lab[3].setBounds(20, 135, 150, 40);
		lab[2].setForeground(Color.BLACK);
		lab[3].setForeground(Color.BLACK);
		but[0].setBounds(35, 230, 100, 30);
		but[1].setBounds(155, 230, 100, 30);
		but[2].setBounds(70, 280, 140, 30);
		
		//USERNAME FIELD
		uname = new JTextField();
		uname.setBounds(20, 90, 245, 35);
		uname.setFont(new Font("MV Boli", Font.PLAIN, 15));
		
		//PASSWORD FIELD
		pword = new JPasswordField();
		pword.setBounds(20, 170, 245, 35);
		pword.setFont(new Font("MV Boli", Font.PLAIN, 15));
		
		//FRAME
		this.setLocationRelativeTo(null);
		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		this.setResizable(false);
		this.setLayout(null);
		this.setSize(new Dimension(300,420));
		this.getContentPane().setBackground(Color.WHITE);
		this.add(uname);
		this.add(pword);
		this.setVisible(true);
	}

	@Override
	public void actionPerformed(ActionEvent e) {
		//THEME BUTTON
		if(e.getSource()==but[2]) {
			if(this.getContentPane().getBackground()==Color.WHITE) {
				this.getContentPane().setBackground(Color.BLACK);
				lab[2].setForeground(Color.WHITE);
				lab[3].setForeground(Color.WHITE);
				but[2].setText("Theme: Dark");
			}
			else{
				this.getContentPane().setBackground(Color.WHITE);
				lab[2].setForeground(Color.BLACK);
				lab[3].setForeground(Color.BLACK);
				but[2].setText("Theme: Light");
			}
		}
		
		//LOGIN BUTTON (READING CREDENTIAL FILES)
		if(e.getSource()==but[0]) {
			try{
			    	BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));
			    	String line;
			    	while ((line = reader.readLine()) != null)
			    	{
			    		if(!line.equals("")){
			    			n = decrypt(line.substring(0,line.indexOf(" ")), 5);
			    			p = decrypt(line.substring(line.indexOf(" ")+3), 5);
			    			if(String.valueOf(uname.getText()).equals("")||String.valueOf(pword.getPassword()).equals("")) {
			    				lab[1].setForeground(Color.red);
								lab[1].setText("Enter Valid Credentials!");
							}
			    			else if(n.equals(uname.getText())) {
								if(p.equals(String.valueOf(pword.getPassword()))) {
									System.out.println("ITS WORKING");
									this.dispose();
									break;
								}
								else {
									lab[1].setForeground(Color.red);
									lab[1].setText("Wrong Password!");
									break;
								}
							}
							else {
								lab[1].setForeground(Color.red);
								lab[1].setText("User Doesn't Exist!");
							}
			    		}
			    	}
			    	reader.close();
			  	}
			catch (Exception e1)
			{}
		}
		
		//SIGN UP BUTTON
		if(e.getSource()==but[1]) {
			if(String.valueOf(uname.getText()).equals("")||String.valueOf(pword.getPassword()).equals("")) {
				lab[1].setForeground(Color.red);
				lab[1].setText("Enter Valid Credentials!");
			}
			else {
				File file = new File("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details");
				if(file.isDirectory()) {
					BufferedReader reader;
					try {
						reader = new BufferedReader(new FileReader("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));
				    	String line;
				    	while ((line = reader.readLine()) != null)
				    	{
				    		if(!line.equals("")){
				    			n = decrypt(line.substring(0,line.indexOf(" ")), 5);
				    			p = decrypt(line.substring(line.indexOf(" ")+3), 5);
				    			if(n.equals(uname.getText())) {
				    				lab[1].setForeground(Color.red);
									lab[1].setText("User already exixt");
									break;
				    			}
				    			else {
				    				appendingText();
				    				lab[1].setForeground(Color.GREEN);
				    				lab[1].setText("Registration Done!");
				    				uname.setText("");
				    				pword.setText("");
				    				break;
				    			}
				    			}
				    		}
					} catch (Exception e1) {
						e1.printStackTrace();
						}
				}
				else {
					file.mkdir();
					appendingText();
					lab[1].setForeground(Color.GREEN);
    				lab[1].setText("Registration Done!");
    				uname.setText("");
    				pword.setText("");
				}
			}
		}
	}
	}



Issues:
* I did not find any issue till now ̶ ̶e̶x̶c̶e̶p̶t̶ ̶w̶e̶a̶k̶ ̶e̶n̶c̶r̶y̶p̶t̶i̶o̶n̶ ̶l̶o̶g̶i̶c̶ ̶(̶y̶o̶u̶ ̶c̶a̶n̶ ̶c̶h̶a̶n̶g̶e̶ ̶i̶t̶ ̶a̶c̶c̶o̶r̶d̶i̶n̶g̶ ̶t̶o̶ ̶y̶o̶u̶r̶s̶e̶l̶f̶)̶

--> You can download the .jar file from release section and import it in Eclipse or IntelliJ IDE.

Thank You for reading till end, please consider checking my other repos too...
