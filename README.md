# Login-Page-with-encryption-java
Login page with data encryption and decryption of credentials.

***************************************************************
v1.5 has been released, check changelogs file for more details.
***************************************************************

This code is solely witten in JAVA by AYUSH and its free to use as long as you don't consider the code as your's.

Details:
This program will show a login page as soon as you run it, and as soon as you enter your credentials and press "Sign Up", it will encrypt your credentials and save it to "C:\Users\username\Documents\Details\Credentials.txt".  ̶N̶o̶t̶e̶ ̶t̶h̶a̶t̶ ̶t̶h̶e̶ ̶e̶n̶c̶r̶y̶p̶t̶i̶o̶n̶ ̶i̶s̶ ̶v̶e̶r̶y̶ ̶b̶a̶s̶i̶c̶ ̶a̶n̶d̶ ̶c̶a̶n̶ ̶b̶e̶ ̶c̶r̶a̶c̶k̶e̶d̶ ̶e̶a̶s̶i̶l̶y̶.̶

Now you can use the same credentials to login (or run the real program) as long as the "Credentials.txt" is not deleted or modified manually. The program will read and decrypt the credentials in the file and compare it to the credentials you entered, if both matches, then it will print "IT'S WORKING!" (You can change the function) and will close the GUI.

Features of the program:
* Can store credentials for future login (Credentials will be encrypted)
* Can save many credentials
* You can use it to create instance of other class and it will work as a login system
* Can change theme of the page (Light and Dark)
* and Many More!

Check some screenshots(v1.5):
![Screenshot (43)](https://user-images.githubusercontent.com/119154806/212009168-afae4c38-4d9a-4e2c-a572-5c9e60549612.png)
![Screenshot (44)](https://user-images.githubusercontent.com/119154806/212009187-93a11672-d039-414d-80e8-fd2cbde40e6e.png)
![Screenshot (45)](https://user-images.githubusercontent.com/119154806/212009199-6f4900d3-d80c-4676-abe1-c38d4d42ff7a.png)
![Screenshot (46)](https://user-images.githubusercontent.com/119154806/212009211-8176ca7d-b9d3-4c0d-823e-25017eea25d7.png)
![Screenshot (47)](https://user-images.githubusercontent.com/119154806/212009423-ea417a27-9869-4588-bafe-e6acee1bbc2e.png)
![Screenshot (48)](https://user-images.githubusercontent.com/119154806/212009281-142620d0-2db1-4ca8-9dc4-31673dd21d85.png)
![Screenshot (49)](https://user-images.githubusercontent.com/119154806/212009297-2ac8cc33-06ea-432e-ab89-f243c29c51ef.png)
![Screenshot (50)](https://user-images.githubusercontent.com/119154806/212009324-6312c2dd-36a3-487d-911d-5591bd3a04d4.png)
![Screenshot (51)](https://user-images.githubusercontent.com/119154806/212009335-ebc716ba-d783-4352-9ac8-7634cb65aafa.png)
![Screenshot (52)](https://user-images.githubusercontent.com/119154806/212009348-5a286645-26d4-4e0c-9242-c3db68417bd3.png)
![Screenshot (53)](https://user-images.githubusercontent.com/119154806/212009365-e2cbbb7b-9c27-4842-b578-329d3b53e553.png)


Details (About Code):
* You can change line 245 to do it what you want to as soon as you login (Create instance of another GUI class and it will launch that)
* The code is easy to understand and its about 400 lines of code
* If you need any help regarding the code, contact me on telegram at @SOUL_AYU

Check out the code (v1.5):

	import java.awt.*;
	import java.awt.event.*;
	import java.io.*;
	import javax.swing.*;

	public class LoginPage extends JFrame implements ActionListener{

	private static final long serialVersionUID = 1L;
	JLabel lab[] = new JLabel[6];
	JTextField uname, code;
	JPasswordField pword;
	JButton but[] = new JButton[5];
	String n,p;
	static String alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";

	//TEXT ENCRYPTION LOGIC
	String encrypt(String plainText, int shiftKey){
	   // plainText = plainText.toLowerCase();
	    String cipherText = "";
	    for (int i = 0; i < plainText.length(); i++){
		int charPosition = alphabet.indexOf(plainText.charAt(i));
		int keyVal = (shiftKey + charPosition) % 52;
		char replaceVal = alphabet.charAt(keyVal);
		cipherText += replaceVal;
	    }
	    return cipherText;
	}

	//TEXT DECRYPTION LOGIC
	public static String decrypt(String cipherText, int shiftKey){
		// cipherText = cipherText.toLowerCase();
		String plainText = "";
		for (int i = 0; i < cipherText.length(); i++){
			int charPosition = alphabet.indexOf(cipherText.charAt(i));
			int keyVal = (charPosition - shiftKey) % 52;
			if (keyVal < 0){
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
			writer.append(encrypt(String.valueOf(uname.getText()), 5)+" : "+encrypt(String.valueOf(pword.getPassword()), 5)+"*"+encrypt(code.getText(),5)+"\n");
			} catch (Exception e) {}
		finally {
			try {
				writer.close();
				} catch (Exception e) {}
			}
		SignUpRevert();
	}

	//FOR HIDING GUI WHILE SIGN UP OR FORGET PASS
	public void hide() {
		if(lab[0].getText().equals("LOGIN PAGE")) {
			but[0].setVisible(false);
			but[3].setVisible(false);
			but[1].setBounds(150, 300, 100, 30);
			code.setBounds(20, 250, 245, 35);
			but[2].setVisible(false);
			lab[1].setText("");
			code.setVisible(true);
			but[4].setVisible(true);
			code.setText("");
		}   
	} 

	//BACK BUTTON INTERNAL LOGIC
	void SignUpRevert() {
		but[1].setBounds(155, 230, 100, 30);
		lab[1].setForeground(Color.GREEN);
		lab[1].setText("Registration done!");
		uname.setText("");
		pword.setText("");
		but[0].setVisible(true);
		but[3].setVisible(true);
		but[1].setBounds(155, 230, 100, 30);
		but[2].setVisible(true);
		lab[0].setText("LOGIN PAGE");
		lab[5].setBounds(20, 215, 150, 40);
		lab[5].setVisible(false);
		code.setVisible(false);
		but[4].setVisible(false);
		lab[2].setText("Username:");
		lab[5].setText("Recovery Key:");
	}

	void replacePass(String newString){
		String oldContent = "";       
		BufferedReader reader = null;       
		FileWriter writer = null;  
		String user, key, pass = null;
		try{
			reader = new BufferedReader(new FileReader("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));
			String line;
			while ((line = reader.readLine()) != null){
				if(!line.equals("")){
					user = decrypt(line.substring(0,line.indexOf(" ")), 5);
					pass = decrypt(line.substring(line.indexOf(" ")+3, line.indexOf("*")), 5);
					key = decrypt(line.substring(line.indexOf("*")+1), 5);
					if(n.equals(user)) {
						line = encrypt(user, 5)+" : "+encrypt(newString, 5)+"*"+encrypt(key, 5);
					}
				oldContent = oldContent + line + "\n";                
			}
			}
			reader.close();
			if(!(pass.equals(newString))) {
				writer = new FileWriter(new File("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));    
				writer.write(oldContent);
				SignUpRevert();
				lab[1].setForeground(Color.GREEN);
				lab[1].setText("Password Modified!");
				lab[5].setVisible(false);
				lab[3].setVisible(true);
				pword.setVisible(true);
				but[1].setText("Sign up");
				writer.close();
			}	
			else {
				lab[1].setText("This is your old password!");
			}
		}
		catch (IOException e){}
	}

	LoginPage(){
		//CREATION OF LABELS
		String labels[] = {"LOGIN PAGE","", "Username:", "Password:", "------------------", "Recovery Key:"};
		String buttons[] = {"Login", "Sign up", "Theme: Light", "Forgot Password?", "<--"};
		for(int i=0; i<6; i++) {
			lab[i] = new JLabel(labels[i]);
			lab[i].setFont(new Font("MV Boli", Font.PLAIN, 15));
			lab[i].setForeground(Color.RED);
			lab[i].setVisible(true);
			this.add(lab[i]);
			if(i<5) {
				but[i] = new JButton(buttons[i]);
				but[i].setForeground(Color.BLACK);
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
	lab[1].setBounds(20, 0, 200, 100);
	lab[1].setFont(new Font("MV Boli", Font.PLAIN, 12));
	lab[2].setBounds(20, 55, 150, 40);
	lab[3].setBounds(20, 135, 150, 40);
	lab[2].setForeground(Color.BLACK);
	lab[5].setForeground(Color.BLACK);
	lab[3].setForeground(Color.BLACK);
	but[0].setBounds(35, 230, 100, 30);
	but[1].setBounds(155, 230, 100, 30);
	but[2].setBounds(70, 320, 140, 30);
	lab[5].setVisible(false);
	but[4].setBounds(30, 300, 100, 30);
	but[4].setVisible(false);
	
	but[3].setBackground(Color.WHITE);
	but[3].setBorder(null);
	but[3].setBounds(40, 275, 200, 30);
	but[3].setForeground(Color.BLUE);
	
	//USERNAME FIELD
	uname = new JTextField();
	uname.setBounds(20, 90, 245, 35);
	uname.setFont(new Font("MV Boli", Font.PLAIN, 15));
	
	//PASSWORD FIELD
	pword = new JPasswordField();
	pword.setBounds(20, 170, 245, 35);
	pword.setFont(new Font("MV Boli", Font.PLAIN, 15));
	
	//USERNAME FIELD
	code = new JTextField();
	code.setBounds(20, 250, 245, 35);
	code.setFont(new Font("MV Boli", Font.PLAIN, 15));
	code.setVisible(false);
	
	//FRAME
	this.setLocationRelativeTo(null);
	this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	this.setResizable(false);
	this.setLayout(null);
	this.setSize(new Dimension(300,420));
	this.getContentPane().setBackground(Color.WHITE);
	this.add(uname);
	this.add(pword);
	this.add(code);
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
				lab[5].setForeground(Color.WHITE);
				but[3].setBackground(Color.BLACK);
				but[2].setText("Theme: Dark");
			}
			else{
				this.getContentPane().setBackground(Color.WHITE);
				lab[2].setForeground(Color.BLACK);
				lab[3].setForeground(Color.BLACK);
				lab[5].setForeground(Color.BLACK);
				but[3].setBackground(Color.WHITE);
				but[2].setText("Theme: Light");
			}
		}
	
	//LOGIN BUTTON (READING CREDENTIAL FILES)
	if(e.getSource()==but[0]) {
		try{
			BufferedReader reader = new BufferedReader(new FileReader("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));
			String line;
			while ((line = reader.readLine()) != null){
				if(!line.equals("")){
					n = decrypt(line.substring(0,line.indexOf(" ")), 5);
					p = decrypt(line.substring(line.indexOf(" ")+3, line.indexOf("*")), 5);
					if(String.valueOf(uname.getText()).equals("")||String.valueOf(pword.getPassword()).equals("")) {
						lab[1].setForeground(Color.red);
						lab[1].setText("Enter valid credentials!");
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
						lab[1].setText("User doesn't exist!");
					}
		    	}
		    }
			reader.close();
		}
		catch (Exception e1){}
	}
	
	//SIGN UP BUTTON
	if(e.getSource()==but[1]) {
		if(but[1].getText().equals("Sign up")) {
			if(lab[0].getText().equals("LOGIN PAGE")) {
				hide();
				lab[0].setText(" REGISTER");
				lab[5].setBounds(20, 215, 150, 40);
				lab[5].setVisible(true);
			}
			else {
				if(String.valueOf(uname.getText()).equals("") || String.valueOf(pword.getPassword()).equals("")) {
					lab[1].setForeground(Color.red);
					lab[1].setText("Enter valid credentials!");
				}
				else if(String.valueOf(pword.getPassword()).contains(" ") || uname.getText().contains(" ")) {
					lab[1].setForeground(Color.red);
					lab[1].setText("Spaces are not allowed!");
				}
				else if(String.valueOf(pword.getPassword()).equals(uname.getText())) {
					lab[1].setForeground(Color.red);
					lab[1].setText("Password must be hard!");
				}
				else if(code.getText().isEmpty()) {
					lab[1].setForeground(Color.red);
					lab[1].setText("Enter recovery key");
				}
				else if(code.getText().equals(uname.getText())) {
					lab[1].setForeground(Color.red);
					lab[1].setText("Key should be hard! Eg. X3ka0");
				}
				else if(code.getText().equals(String.valueOf(pword.getPassword()))) {
					lab[1].setForeground(Color.red);
					lab[1].setText("Key should differ from password!");
				}
				else {
					File file = new File("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details");
					if(file.isDirectory()) {
						BufferedReader reader;
						try {
							reader = new BufferedReader(new FileReader("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));
							String line;
							while ((line = reader.readLine()) != null){
								if(!line.isEmpty()){
									n = decrypt(line.substring(0,line.indexOf(" ")), 5);
									lab[1].setText("");
									if(n.equals(uname.getText())) {
					    				lab[1].setForeground(Color.red);
										lab[1].setText("User already exist");
										break;
									}	
								}
				    		}
							if(!(lab[1].getText().equals("User already exist"))) {
								appendingText();
								lab[1].setForeground(Color.GREEN);
								lab[1].setText("Registration done!");
								uname.setText("");
								pword.setText("");
							}	
						} catch (Exception e1) {}
					}
					else {
						file.mkdir();
						appendingText();
					}
				}
			}
		}
		else if(!(lab[2].getText().equals("New Password"))){
			File file = new File("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details");
			if(file.isDirectory()) {
				BufferedReader reader = null;
				try {
					reader = new BufferedReader(new FileReader("C:\\Users\\"+System.getProperty("user.name")+"\\Documents\\Details\\Credentials.txt"));
					String line;
					while ((line = reader.readLine()) != null){
						if(!line.equals("")){
							n = decrypt(line.substring(0,line.indexOf(" ")), 5);
							p = decrypt(line.substring(line.indexOf("*")+1), 5);
							if(String.valueOf(uname.getText()).equals("") || String.valueOf(code.getText()).equals("")) {
			    				lab[1].setForeground(Color.red);
								lab[1].setText("Enter valid credentials!");
							}
			    			else if(n.equals(uname.getText())) {
								if(p.equals(String.valueOf(code.getText()))) {
									lab[1].setText("");
									uname.setText("");
									code.setText("");
									lab[2].setText("New Password");
									lab[5].setText("Confirm Password");
									break;
								}
								else {
									lab[1].setForeground(Color.red);
									lab[1].setText("Incorrect key entered!");
									break;
								}
							}
							else {
								lab[1].setForeground(Color.red);
								lab[1].setText("User doesn't exist!");
							}		
						}	
					}
					reader.close();
					} catch (IOException e1) {}
				}
			}
		else {
			if(!(uname.getText().equals(code.getText()))){
				lab[1].setForeground(Color.RED);
				lab[1].setText("Password should match!");
			}
			else if(uname.getText().contains(" ")){
				lab[1].setForeground(Color.RED);
				lab[1].setText("Spaces are not allowed!");
			}
			else if(uname.getText().contains("*")){
				lab[1].setForeground(Color.RED);
				lab[1].setText("* is not allowed!");
			}
			else if(uname.getText().equals(code.getText())) {
				replacePass(uname.getText());
			}
		}
	}
	
	if(e.getSource()==but[3]) {
		hide();
		lab[0].setText(" RECOVERY");
		lab[5].setBounds(20, 120, 150, 40);
		code.setBounds(20, 155, 245, 35);
		lab[5].setVisible(true);
		lab[3].setVisible(false);
		pword.setVisible(false);
		but[1].setText("Proceed");
	}
	
	if(e.getSource()==but[4]) {
		SignUpRevert();
		lab[1].setText("");
		lab[5].setVisible(false);
		lab[3].setVisible(true);
		pword.setVisible(true);
		but[1].setText("Sign up");
	}
	}
}

Issues:
* I did not find any issue till now ̶ ̶e̶x̶c̶e̶p̶t̶ ̶w̶e̶a̶k̶ ̶e̶n̶c̶r̶y̶p̶t̶i̶o̶n̶ ̶l̶o̶g̶i̶c̶ ̶(̶y̶o̶u̶ ̶c̶a̶n̶ ̶c̶h̶a̶n̶g̶e̶ ̶i̶t̶ ̶a̶c̶c̶o̶r̶d̶i̶n̶g̶ ̶t̶o̶ ̶y̶o̶u̶r̶s̶e̶l̶f̶)̶

--> You can download the .jar file from release section and import it in Eclipse or IntelliJ IDE.

Thank You for reading till end, please consider checking my other repos too...
