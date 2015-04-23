import java.awt.Dimension;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.table.DefaultTableCellRenderer;
import javax.swing.table.DefaultTableModel;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartPanel;
import org.jfree.chart.JFreeChart;
import org.jfree.data.xy.XYSeries;
import org.jfree.data.xy.XYSeriesCollection;

import net.miginfocom.swing.MigLayout;




public class Main {
	public static void main(String[] args)  {
		//creating the frame
		JFrame frame = new JFrame("Lorenz Chaos");
		frame.setPreferredSize(new Dimension(800,400));
		
		//lets see if it finds anything different
		
		//Vega
		JLabel vegaText=new JLabel();
		vegaText.setText ("Enter vega:"); 
		final JTextField vega=new JTextField(10);
		vega.setPreferredSize( new Dimension( 25, 25 ) );
		
		//beta
		JLabel betaText=new JLabel();
		betaText.setText ("Enter beta:"); 
		final JTextField beta=new JTextField(10);
		beta.setPreferredSize( new Dimension( 25, 25 ) );
		
		//rho
		JLabel rhoText=new JLabel();
		rhoText.setText ("Enter rho:"); 
		final JTextField rho=new JTextField(10);
		rho.setPreferredSize( new Dimension( 25, 25 ) );
		
		//x0
		JLabel x0Text=new JLabel();
		x0Text.setText ("Enter x-start:"); 
		final JTextField x0=new JTextField(10);
		x0.setPreferredSize( new Dimension( 25, 25 ) );
		
		//y0
		JLabel y0Text=new JLabel();
		y0Text.setText ("Enter y-start:"); 
		final JTextField y0=new JTextField(10);
		y0.setPreferredSize( new Dimension( 25, 25 ) );
		
		//z0
		JLabel z0Text=new JLabel();
		z0Text.setText ("Enter z-start:"); 
		final JTextField z0=new JTextField(10);
		z0.setPreferredSize( new Dimension( 25, 25 ) );
		
		//StepSize
		JLabel stepSizeText=new JLabel();
		stepSizeText.setText ("Enter Step size:"); 
		final JTextField stepSize=new JTextField(10);
		stepSize.setPreferredSize( new Dimension( 25, 25 ) );
		
		
		final DefaultTableModel model = new DefaultTableModel(); 
		final JTable table = new JTable(model);
		model.addColumn("time"); 
		model.addColumn("x"); 
		model.addColumn("y");
		model.addColumn("z");
		
		
		DefaultTableCellRenderer centerRenderer = new DefaultTableCellRenderer();
		centerRenderer.setHorizontalAlignment( JLabel.CENTER );
		table.getColumnModel().getColumn(0).setCellRenderer( centerRenderer );
		table.getColumnModel().getColumn(1).setCellRenderer( centerRenderer );
		
		
		JScrollPane scrollPane = new JScrollPane(table);	
		
		//Creating Chart data set

		final XYSeriesCollection dataset = new XYSeriesCollection();
		

		
		
		JButton calcButton = new JButton("Calculate");
		calcButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {

           
            	deleteAllRows(model);
            	
                //Get Number
            	int steps=0;
            	
        		String vegatext = vega.getText();
        		double vega= Integer.parseInt(vegatext);

        		String rhotext = rho.getText();
        		double rho= Integer.parseInt(rhotext);
        		
        		String betatext = beta.getText();
        		double beta= Integer.parseInt(betatext);
        		
        		String x0text = x0.getText();
        		double x0= Integer.parseInt(x0text);

        		String y0text = y0.getText();
        		double y0= Integer.parseInt(y0text);
        		
        		String z0text = z0.getText();
        		double z0= Integer.parseInt(z0text);
        		
        		String stepSizetext = stepSize.getText();
        		Double stepSize = Double.parseDouble(stepSizetext);
        		
        		boolean autoSort = false;
            	XYSeries Chaos = new XYSeries("Chaos",autoSort);
        		
        		
        		Object [] InitialObject = new Object[4];
        		InitialObject[0] = 0;
        		InitialObject[1] = x0;
        		InitialObject[2] = y0;
        		InitialObject[3] = z0;
        		
        		model.addRow(InitialObject);
        		
        		double x=x0;
        		double y=y0;
        		double z=z0;
        		double t=0;
        		double xchaos=0;
        		double zchaos=0;		
        		
        		
        		int max=10000;
        		int i=0;
        		while(max>i){
                	Object [] iteration = new Object[4];
                	
                	iteration=RK4(t,x,y,z,vega,rho,beta,stepSize);

                	Double x1=(Double) iteration[1];
                	x =x1.doubleValue();
                	Double y1=(Double) iteration[2];
                	y =y1.doubleValue();
                	Double z1=(Double) iteration[3];
                	z = z1.doubleValue();
                	Double t1=(Double) iteration[0];
                	t =t1.doubleValue();

                	
                	Chaos.add(x,z);
              
                	model.addRow(iteration);

        			i++;
               	}
                
        		table.repaint();
        		dataset.addSeries(Chaos);

            }
        });
		
		
		JButton clearButton = new JButton("Clear Graph");
		clearButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
            	            	
            	dataset.removeAllSeries();
            }
            });
	
		//Create chart
		JFreeChart yxLineChart = ChartFactory.createXYLineChart("Chaos", "Step", "Number", dataset);
		ChartPanel chartPanel = new ChartPanel( yxLineChart );
		
		
	    MigLayout lm = new MigLayout("nogrid, fillx");
	    JPanel migPanel = new JPanel(lm);
		
	    migPanel.add(vegaText);
	    migPanel.add(vega);
	    migPanel.add(rhoText);
	    migPanel.add(rho);
	    migPanel.add(betaText);
	    migPanel.add(beta);
	    migPanel.add(x0Text);
	    migPanel.add(x0);	    
	    migPanel.add(y0Text);
	    migPanel.add(y0);	
	    migPanel.add(z0Text);
	    migPanel.add(z0);	
	    migPanel.add(stepSizeText);
	    migPanel.add(stepSize,"wrap");	
	    
	    migPanel.add(calcButton);
	    migPanel.add(clearButton, "Wrap");
	    migPanel.add(scrollPane);
	    migPanel.add(chartPanel);
	    
		frame.add(migPanel);
		frame.pack();  
		frame.setVisible(true);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

	
}
	
	public static void deleteAllRows(final DefaultTableModel model) {
	    for( int i = model.getRowCount() - 1; i >= 0; i-- ) {
	        model.removeRow(i);
	    }
	}
	
	

//-----------the equations ------------------
public static double dxdt(double t, double x, double y, double z, double vega){
	return vega*(y-x);
} 
public static double dydt(double t, double x, double y, double z, double rho){
	return -x*z+rho*x-y;
} 
public static double dzdt(double t, double x, double y, double z, double beta){
	return x*y-beta*z;
} 

//----------------RK4----------------------


public static Object[] RK4(double t, double x, double y, double z, double vega, double rho, double beta, double h){
	double k1x, k1y,k1z, k2x,k2y,k2z,k3x,k3y,k3z,k4x,k4y,k4z;
	k1x=h*dxdt(t,x,y,z,vega);
	k1y=h*dydt(t,x,y,z,rho);
	k1z=h*dzdt(t,x,y,z,beta);
	System.out.println(k1x);
	
	k2x=h*dxdt(t+h/2,x+k1x/2,y+k1y/2,z+k1z/2,vega);
	k2y=h*dydt(t+h/2,x+k1x/2,y+k1y/2,z+k1z/2,rho);
	k2z=h*dzdt(t+h/2,x+k1x/2,y+k1y/2,z+k1z/2,beta);
	
	k3x=h*dxdt(t+h/2,x+k2x/2,y+k2y/2,z+k2z/2,vega);
	k3y=h*dydt(t+h/2,x+k2x/2,y+k2y/2,z+k2z/2,rho);
	k3z=h*dzdt(t+h/2,x+k2x/2,y+k2y/2,z+k2z/2,beta);
	
	k4x=h*dxdt(t+h,x+k3x,y+k3y,z+k3z,vega);
	k4y=h*dydt(t+h,x+k3x,y+k3y,z+k3z,rho);
	k4z=h*dzdt(t+h,x+k3x,y+k3y,z+k3z,beta);
	
	
	   x = x + (k1x + 2*k2x + 2*k3x + k4x) / 6;
	   y = y + (k1y + 2*k2y + 2*k3y + k4y) / 6;
	   z = z + (k1z + 2*k2z + 2*k3z + k4z) / 6;
	   t=t+h;
	   
		Object [] RH4 = new Object[4];
	
		RH4[0]=t;
		RH4[1]=x;
		RH4[2]=y;
		RH4[3]=z;
	return RH4;
}







	
}