import com.sun.pdfview.*;

import java.awt.*;
import java.awt.event.*;

import java.io.*;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

import javax.swing.*;


class PDFView {
    private static PDFPage page;
    private static PagePanel panel;
    private static PDFFile pdffile;
    private static int nbpage=1;
    public static void setup(String s) throws IOException {
        JFrame frame = new JFrame(s);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        panel = new PagePanel();
        frame.add(panel);
        frame.pack();
        frame.setVisible(true);
        File file = new File(s);
        @SuppressWarnings("resource")
	    RandomAccessFile raf = new RandomAccessFile(file,"r");
        FileChannel channel = raf.getChannel();
        ByteBuffer buf = channel.map(FileChannel.MapMode.READ_ONLY, 0, channel.size());
        pdffile = new PDFFile(buf);
        page = pdffile.getPage(nbpage);
        panel.showPage(page);
    }
    static void PageSuivante(){
    	if(nbpage!=pdffile.getNumPages()){
	    nbpage++;
	    page=pdffile.getPage(nbpage);
	    panel.showPage(page);
    	}
    }
    static void PagePrecedente(){
    	if(nbpage!=1){
	    nbpage--;
	    page=pdffile.getPage(nbpage);
	    panel.showPage(page);
    	}
    }
    public static void main(final String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
		public void run() {
		    try {
			//arborescence du fichier
			System.out.println("Entrez l'arboresence du fichier :");
			InputStreamReader isr=new InputStreamReader(System.in);
			BufferedReader br=new BufferedReader(isr);
                	String s=br.readLine();
                	PDFView.setup(s);
                	Frame f = new CadreBoutons();
                	f.setVisible(true);
		    } catch (IOException ex) {
			ex.printStackTrace();
		    }
		}
	    });
    }
}
class CadreBoutons extends Frame {
	public CadreBoutons(){
		setTitle("Controleur");
		setSize(200,100);
		addWindowListener(new Fermeture());
		add(new Panneau());
	}
}
class Fermeture extends WindowAdapter {
	public void windowClosing(WindowEvent e) {
		System.exit(0);
	}
}
class Panneau extends Panel implements ActionListener{
    Button precedent,suivant;
    public Panneau(){
	precedent=new Button("Précédent");
	suivant=new Button("Suivant");
	add(precedent);
	add(suivant);
	precedent.addActionListener(this);
	suivant.addActionListener(this);
    }
    public void actionPerformed(ActionEvent e){
	Object o = e.getSource();
	if(o==precedent){
	    PDFView.PagePrecedente();
	}
	if(o==suivant){
	    PDFView.PageSuivante();
	}
    }
}
