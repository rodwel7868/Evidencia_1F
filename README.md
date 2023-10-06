# Evidencia_1F
Evidencia 
package citasmedicas;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class ClasePrincipal {
    private static final String DB_FOLDER = "db/";
    private static final String DOCTORES_FILE = DB_FOLDER + "doctores.csv";
    private static final String PACIENTES_FILE = DB_FOLDER + "pacientes.csv";
    private static final String CITAS_FILE = DB_FOLDER + "citas.csv";
    private static final String ADMIN_USERNAME = "admin";
    private static final String ADMIN_PASSWORD = "Rodwel1234";

    private List<Doctor> doc;
    private List<Paciente> pac;
    private List<Cita> cit;
    private Scanner sc;

    public ClasePrincipal() {
        doc = new ArrayList<>();
        pac = new ArrayList<>();
        cit = new ArrayList<>();
        sc = new Scanner(System.in);
        crearCarpetaDBSiNoExiste();
    }
    private void crearCarpetaDBSiNoExiste() {
        Path dbFolderPath = Paths.get(DB_FOLDER);
        if (!Files.exists(dbFolderPath)) {
            try {
                Files.createDirectories(dbFolderPath);
            } catch (IOException e) {
                System.out.println("Error al crear la carpeta 'db': " + e.getMessage());
            }
        }
    }


    public void ejecutar() {
        System.out.println("Bienvenido al sistema de citas medicas.");

        if (!autenticarAdministrador()) {
            System.out.println("Usuario o contraseña incorrecto. Intenta de nuevo.");
            ejecutar();
            return;
        }

        cargarDatos();

        int op;
        do {
            mostrarMenu();
            op = sc.nextInt();
            sc.nextLine();

            switch (op) {
                case 1:
                    altaDoctor();
                    break;
                case 2:
                    altaPaciente();
                    break;
                case 3:
                    crearCita();
                    break;
                case 4:
                    listarCitas();
                    break;
                case 0:
                    break;
                default:
                    System.out.println("Opción inválida. Por favor, seleccione la opción correcta.");
                    break;
            }
        } while (op != 0);

        sc.close();
        System.out.println("¡Gracias por su visita, hasta pronto!");
    }

    private boolean autenticarAdministrador() {
        System.out.println("Por favor, ingrese usuario y contraseña.");

        System.out.print("Usuario: ");
        String username = sc.nextLine();

        System.out.print("Contraseña: ");
        String password = sc.nextLine();

        return username.equals(ADMIN_USERNAME) && password.equals(ADMIN_PASSWORD);
    }

    private void cargarDatos() {
        cargarDoctores();
        cargarPacientes();
        cargarCitas();
    }

    private void cargarDoctores() {
        try (BufferedReader br = new BufferedReader(new FileReader(DOCTORES_FILE))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] data = line.split(",");
                int id = Integer.parseInt(data[0]);
                String nombre = data[1];
                String especialidad = data[2];
                Doctor doctor = new Doctor(id, nombre, especialidad);
                doc.add(doctor);
            }
        } catch (IOException e) {
            System.out.println("Error al cargar datos del doctor. " + e.getMessage());
        }
    }

    private void cargarPacientes() {
        try (BufferedReader br = new BufferedReader(new FileReader(PACIENTES_FILE))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] data = line.split(",");
                int id = Integer.parseInt(data[0]);
                String nombre = data[1];
                Paciente paciente = new Paciente(id, nombre);
                pac.add(paciente);
            }
        } catch (IOException e) {
            System.out.println("Error al cargar datos del paciente. " + e.getMessage());
        }
    }

    private void cargarCitas() {
        try (BufferedReader br = new BufferedReader(new FileReader(CITAS_FILE))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] data = line.split(",");
                int id = Integer.parseInt(data[0]);
                String fechaHora = data[1];
                String motivo = data[2];
                int doctorId = Integer.parseInt(data[3]);
                int pacienteId = Integer.parseInt(data[4]);
                Cita cita = new Cita(id, fechaHora, motivo, doctorId, pacienteId);
                cit.add(cita);
            }
        } catch (IOException e) {
            System.out.println("Error al cargar datos de cita. " + e.getMessage());
        }
    }

    private void altaDoctor() {
        System.out.println("Ingrese datos del doctor.");

        int id = generarNuevoIdDoctor(); // Generar nuevo identificador único

        System.out.print("Nombre completo: ");
        String nombre = sc.nextLine();

        System.out.print("Especialidad: ");
        String especialidad = sc.nextLine();

        Doctor doctor = new Doctor(id, nombre, especialidad);
        doc.add(doctor);
        System.out.println("Registro exitoso de doctor.");
        guardarDoctores();
    }
    private int generarNuevoIdDoctor() {
        if (doc.isEmpty()) {
            return 1;
        } else {
            int ultimoId = doc.get(doc.size() - 1).getId();
            return ultimoId + 1;
        }
    }

    private void altaPaciente() {
        System.out.println("Ingrese datos del paciente.");

        int id = generarNuevoIdPaciente();

        System.out.print("Nombre completo: ");
        String nombre = sc.nextLine();

        Paciente paciente = new Paciente(id, nombre);
        pac.add(paciente);
        System.out.println("Registro exitoso de paciente.");
        guardarPacientes();
    }
    private int generarNuevoIdPaciente() {
        if (pac.isEmpty()) {
            return 1;
        } else {
            int ultimoId = pac.get(pac.size() - 1).getId();
            return ultimoId + 1;
        }
    }
    private void crearCita() {
        System.out.println("Ingrese datos de cita.");

        int id = generarNuevoIdCrearCita();

        System.out.print("Fecha y hora (dd/mm/aaaa hh:mm): ");
        String fechaHora = sc.nextLine();

        System.out.print("Motivo de la cita: ");
        String motivo = sc.nextLine();

        System.out.println("Seleccione el doctor:");
        listarDoctores();

        System.out.print("Id del doctor: ");
        int doctorId = sc.nextInt();
        sc.nextLine();

        System.out.println("Seleccione el paciente:");
        listarPacientes();

        System.out.print("Id del paciente: ");
        int pacienteId = sc.nextInt();
        sc.nextLine();

        Cita cita = new Cita(id, fechaHora, motivo, doctorId, pacienteId);
        cit.add(cita);
        System.out.println("Cita creada exitosamente.");
        guardarCitas();
    }
    private int generarNuevoIdCrearCita() {
        if (cit.isEmpty()) {
            return 1;
        } else {
            int ultimoId = cit.get(cit.size() - 1).getId();
            return ultimoId + 1;
        }
    }

    private void listarCitas() {
        System.out.println("Lista de citas:");

        for (Cita cita : cit) {
            System.out.println(cita);
        }
    }

    private void listarDoctores() {
        for (Doctor doctor : doc) {
            System.out.println(doctor);
        }
    }

    private void listarPacientes() {
        for (Paciente paciente : pac) {
            System.out.println(paciente);
        }
    }

    private void guardarDoctores() {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(DOCTORES_FILE))) {
            for (Doctor doctor : doc) {
                bw.write(doctor.getId() + "," + doctor.getNombre() + "," + doctor.getEspecialidad());
                bw.newLine();
            }
        } catch (IOException e) {
            System.out.println("Error al almacenar al doctor: " + e.getMessage());
        }
    }

    private void guardarPacientes() {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(PACIENTES_FILE))) {
            for (Paciente paciente : pac) {
                bw.write(paciente.getId() + "," + paciente.getNombre());
                bw.newLine();
            }
        } catch (IOException e) {
            System.out.println("Error al almacenar al pacientes: " + e.getMessage());
        }
    }

    private void guardarCitas() {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(CITAS_FILE))) {
            for (Cita cita : cit) {
                bw.write(cita.getId() + "," + cita.getFechaHora() + "," + cita.getMotivo()
                        + "," + cita.getDoctorId() + "," + cita.getPacienteId());
                bw.newLine();
            }
        } catch (IOException e) {
            System.out.println("Error al almacenar datos de cita: " + e.getMessage());
        }
    }


    private void mostrarMenu() {
        System.out.println();
        System.out.println("Seleccione una opción:");
        System.out.println("1. Alta de doctores");
        System.out.println("2. Alta de pacientes");
        System.out.println("3. Agendar una cita con fecha y hora");
        System.out.println("4. Listas de citas");
        System.out.println("0. Salir");
        System.out.print("Opción: ");
    }
    public static void main(String[] args) {
        ClasePrincipal consultorio = new ClasePrincipal();
        consultorio.ejecutar();
    }
}

