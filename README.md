import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class AplikasiKalkulatorKeuangan {

    // Membuat JFrame sebagai wadah utama aplikasi
    private JFrame frame;

    // Panel untuk input pengeluaran
    private JPanel panelPengeluaran;
    private JLabel labelPengeluaran;
    private JTextField textFieldPengeluaran;

    // Panel untuk input tabungan
    private JPanel panelTabungan;
    private JLabel labelTabungan;
    private JTextField textFieldTabungan;

    // Panel untuk menampilkan hasil rencana anggaran
    private JPanel panelRencana;
    private JLabel labelRencana;
    private JTextField textFieldRencana;

    // Tombol untuk melakukan perhitungan
    private JButton buttonHitung;

    // Konstruktor AplikasiKalkulatorKeuangan
    public AplikasiKalkulatorKeuangan() {
        // Inisialisasi frame
        frame = new JFrame("Aplikasi Kalkulator Keuangan");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Panel untuk input pengeluaran
        panelPengeluaran = new JPanel(new FlowLayout());
        labelPengeluaran = new JLabel("Pengeluaran: ");
        textFieldPengeluaran = new JTextField(20);
        panelPengeluaran.add(labelPengeluaran);
        panelPengeluaran.add(textFieldPengeluaran);

        // Panel untuk input tabungan
        panelTabungan = new JPanel(new FlowLayout());
        labelTabungan = new JLabel("Tabungan: ");
        textFieldTabungan = new JTextField(20);
        panelTabungan.add(labelTabungan);
        panelTabungan.add(textFieldTabungan);

        // Panel untuk menampilkan hasil rencana anggaran
        panelRencana = new JPanel(new FlowLayout());
        labelRencana = new JLabel("Rencana Anggaran: ");
        textFieldRencana = new JTextField(20);
        // Membuat textFieldRencana tidak dapat diubah
        textFieldRencana.setEditable(false);
        panelRencana.add(labelRencana);
        panelRencana.add(textFieldRencana);

        // Tombol untuk melakukan perhitungan
        buttonHitung = new JButton("Hitung");
        buttonHitung.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                hitungRencanaAnggaran();
            }
        });

        // Panel khusus untuk tombol
        JPanel panelButton = new JPanel(new FlowLayout());
        panelButton.add(buttonHitung);

        // Menambahkan panel-panel ke frame menggunakan BorderLayout
        frame.add(panelPengeluaran, BorderLayout.NORTH);
        frame.add(panelTabungan, BorderLayout.CENTER);
        frame.add(panelRencana, BorderLayout.SOUTH);
        frame.add(panelButton, BorderLayout.WEST);

        // Mengatur ukuran frame
        frame.setSize(400, 300);
        // Membuat frame menjadi terlihat
        frame.setVisible(true);
    }

    // Metode untuk melakukan perhitungan rencana anggaran
    private void hitungRencanaAnggaran() {
        try {
            // Mengambil nilai pengeluaran dan tabungan dari input user
            int pengeluaran = Integer.parseInt(textFieldPengeluaran.getText());
            int tabungan = Integer.parseInt(textFieldTabungan.getText());

            // Melakukan perhitungan rencana anggaran
            double rencanaAnggaran = (double) tabungan / (double) pengeluaran;

            // Menampilkan hasil rencana anggaran pada textFieldRencana
            textFieldRencana.setText(String.format("%.2f", rencanaAnggaran));
        } catch (NumberFormatException ex) {
            // Menangkap exception jika input bukan angka
            JOptionPane.showMessageDialog(frame, "Masukkan angka yang valid untuk Pengeluaran dan Tabungan.");
        }
    }

    // Metode main untuk menjalankan aplikasi
    public static void main(String[] args) {
        // Menjalankan aplikasi dalam EDT (Event Dispatch Thread)
        SwingUtilities.invokeLater(() -> new AplikasiKalkulatorKeuangan());
    }
}
