# etude
Some of the basic practice learning JAVA
//:Example6_8.java
/*ÒÆ¶¯·½¿é*/
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

/**Push box game originally conceived
*Control object movement
*@author Pluto
*@version 1.0
*/

public class Example6_8 extends JFrame implements ActionListener
{
	private JButton left = new JButton("Ïò×óÒÆ");               //´´½¨°´Å¥
	private JButton right = new JButton("ÏòÓÒÒÆ");
	private JButton up = new JButton("ÏòÉÏÒÆ");
	private JButton down = new JButton("ÏòÏÂÒÆ");
	
	public MoveCanvas drawing = new MoveCanvas();            //ÊµÀý»¯»­²¼£¬»æÖÆÍ¼ÐÎ¿é
	
	private class WindowCloser extends WindowAdapter
	{
		public void windowClosing(WindowEvent we)
		{System.exit(0);}
		}
		public Example6_8()
		{
			super("ÒÆ¶¯·½¿é");
			setSize(400,400);
			setVisible(true);
			Panel p = new Panel();
			p.setLayout(new FlowLayout());
			setLayout(new BorderLayout());
			add (p,BorderLayout.SOUTH);
			add (drawing,BorderLayout.CENTER);
			p.add(up);  p.add(down);
			p.add(left);  p.add(right);
			validate();
			left.addActionListener(this);                            //°´Å¥Ïò¼àÊÓÆ÷×¢²á£¬ÊµÏÖ¼àÌý½Ó¿Ú
			right.addActionListener(this);
			up.addActionListener(this);
			down.addActionListener(this);
			addWindowListener(new WindowCloser());
			}
		public void actionPerformed(ActionEvent e)              //°´Å¥¿ØÖÆÍ¼ÐÎ¿éµÄÒÆ¶¯·½Ïò£¬Æä·½·¨ÔÚ»­²¼ÀàÖÐµÄ¶¨Òå
		{
			if(e.getSource() == up)
			drawing.moveUp();
			else if(e.getSource() == down)
			drawing.moveDown();
			else if(e.getSource() == right)
			drawing.moveRight();
			else if(e.getSource() == left)
			drawing.moveLeft();
			}
		public static void main (String args[])
		{
			/**Sole entry point to class & application
			*@param args arry of string arguments
			*@return No return value
			*@exception exceptions N0 exceptions thrown
			*/
			JFrame. setDefaultLookAndFeelDecorated(true);
			new Example6_8();
			}
	}
	
	//´´½¨Ò»¸ö»æÖÆ¿ÉÒÆ¶¯µÄ·½¿é»­²¼Àà
	class MoveCanvas extends Canvas               //¶¨Òå»æÖÆ¿ÉÒÆ¶¯µÄ·½¿é»­²¼Àà
	{
		int WIDTH = 30,HEIGHT = 30,INC = 10;             //ÉèÖÃ·½¿é´óÐ¡£¬INCÎªÃ¿´ÎÒÆ¶¯·½¿éµÄ²½³¤Öµ
		int i,j;
		public void  paint(Graphics g)          //»æÖÆºìÉ«ºÚ±ßµÄ·½¿é£¬ÆäÎ»ÖÃËæi£¬j±ä»¯£¬´Ó¶ø¿ÉÒÔÒÆ¶¯
		{
			g.drawRect(0,0,getSize().width - 1,getSize().height - 1);
			g.setColor(Color.black);
			g.fillRect(i + 2,j + 2,WIDTH + 2,HEIGHT + 2);
			g.setColor(Color.red);
			g.fillRect(i,j,WIDTH,HEIGHT);
			}
		public void moveUp()                  //Í¼ÐÎ¿éÎ»ÖÃÔÚ´¹Ö±·½ÏòÔö¼Ó£¬´Ó¶øÊµÏÖÍ¼ÐÎ¿éÏò×óÒÆ¶¯
		{
			if(j > 0)
			j -= INC;
			else
			j = getSize().height - INC;
			repaint();
			}
		public void moveDown()                 //Í¼ÐÎ¿éÎ»ÖÃÔÚ´¹Ö±·½ÏòÔö¼Ó£¬´Ó¶øÊµÏÖÍ¼ÐÎ¿éÏòÏÂÒÆ¶¯
		{
			if(j < getSize().height - INC)
			j += INC;
			else
			j = 0;
			repaint();
			}
		public void moveLeft()                 //Í¼ÐÎ¿éÎ»ÖÃÔÚË®Æ½·½Ïò¼õÉÙ£¬´Ó¶øÊµÏÖÍ¼ÐÎ¿éÏò×óÒÆ¶¯
		{
			if(i > 0)
			i -= INC;
			else
			i = getSize().width-INC;
			repaint();
			}
		public void moveRight()                //Í¼ÐÎ¿éÎ»ÖÃÔÚË®Æ½·½ÏòÔö¼Ó£¬´Ó¶øÊµÏÖÍ¼ÐÎ¿éÏòÓÒÒÆ¶¯
		{
			if(i < getSize().width - INC)
			i += INC;
			else
			i = 0;
			repaint();
			}
		}
