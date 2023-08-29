# ReportRape
GUI
package report;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.UUID;


/**
 *
 * @author zintlemgqongose
 */


public class gui extends JFrame {
    private JTextField txtReportId;
    private JTextArea txaFollowUp;
    private JComboBox<String> cmbStatus;
    private JButton btnSubmit;
    private JButton btnPrevious;
    private JTextField txtIncidentId;
    private JTextField txtVictimId;
    private JTextField txtIncidentDate;
    private JTextField txtAgencyId;

    public gui() {
        super("Rape Report Follow-up");
        setLayout(new BorderLayout());

        JPanel inputPanel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.insets = new Insets(5, 5, 5, 5);

        txtReportId = new JTextField(15);
        txtReportId.setEditable(false);
        addLabelAndComponent(inputPanel, gbc, "Report ID:", txtReportId);

        txaFollowUp = new JTextArea(5, 15);
        addLabelAndComponent(inputPanel, gbc, "Follow-up:", new JScrollPane(txaFollowUp));

        String[] statusOptions = {"In Progress", "Completed", "Pending"};
        cmbStatus = new JComboBox<>(statusOptions);
        addLabelAndComponent(inputPanel, gbc, "Status:", cmbStatus);

        txtIncidentId = new JTextField(15);
        txtIncidentId.setEditable(false);
        addLabelAndComponent(inputPanel, gbc, "Incident ID:", txtIncidentId);

        txtVictimId = new JTextField(15);
        txtVictimId.setEditable(false);
        addLabelAndComponent(inputPanel, gbc, "Victim ID:", txtVictimId);

        txtIncidentDate = new JTextField(15);
        txtIncidentDate.setEditable(false);
        addLabelAndComponent(inputPanel, gbc, "Incident Date:", txtIncidentDate);

        txtAgencyId = new JTextField(15);
        txtAgencyId.setEditable(false);
        addLabelAndComponent(inputPanel, gbc, "Agency ID:", txtAgencyId);

        JPanel buttonPanel = new JPanel();
        btnSubmit = new JButton("Submit");
        btnPrevious = new JButton("Previous");

        
        btnSubmit.setBackground(new Color(63, 127, 191));
        btnSubmit.setForeground(Color.PINK);
        btnSubmit.setFont(new Font("Arial", Font.BOLD, 14));

        
        btnPrevious.setBackground(new Color(63, 127, 191));
        btnPrevious.setForeground(Color.BLUE);
        btnPrevious.setFont(new Font("Arial", Font.BOLD, 14));

        buttonPanel.add(btnSubmit);
        buttonPanel.add(btnPrevious);

        btnSubmit.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                navigateToSubmit();
            }
        });

        btnPrevious.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                navigateToPrevious();
            }
        });

        String uniqueReportId = generateUniqueReportId();
        txtReportId.setText(uniqueReportId);

        String uniqueIncidentId = generateUniqueIncidentId();
        txtIncidentId.setText(uniqueIncidentId);

        String uniqueVictimId = generateUniqueVictimId();
        txtVictimId.setText(uniqueVictimId);

        String IncidentDate = generateCurrentDateTime();
        txtIncidentDate.setText(IncidentDate);

        String uniqueAgencyId = generateUniqueAgencyId();
        txtAgencyId.setText(uniqueAgencyId);

        add(inputPanel, BorderLayout.CENTER);
        add(buttonPanel, BorderLayout.SOUTH);
    }

    private void addLabelAndComponent(JPanel panel, GridBagConstraints gbc, String label, JComponent component) {
        gbc.gridx = 0;
        gbc.gridy++;
        panel.add(new JLabel(label), gbc);

        gbc.gridx = 1;
        panel.add(component, gbc);
    }

    private String generateUniqueReportId() {
        return UUID.randomUUID().toString();
    }

    private String generateUniqueIncidentId() {
        return "INC" + UUID.randomUUID().toString().substring(0, 8);
    }

    private String generateUniqueVictimId() {
        return "VIC" + UUID.randomUUID().toString().substring(0, 8);
    }

    private String generateUniqueAgencyId() {
        return "AGC" + UUID.randomUUID().toString().substring(0, 8);
    }

    private String generateCurrentDateTime() {
        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        return now.format(formatter);
    }

    private void navigateToSubmit() {
        JOptionPane.showMessageDialog(this, "Thank you, your Report has been submitted successfully.");
    }

    private void navigateToPrevious() {
        JOptionPane.showMessageDialog(this, "Navigating to previous page?");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            gui gui = new gui();
            gui.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            gui.setSize(400, 500);
            gui.setVisible(true);
        });
    }
}
