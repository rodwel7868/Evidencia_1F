# Evidencia_1F
Evidencia 
package citasmedicas;

import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

class Administrador extends Usuario {
    public Administrador(String identificador, String contrasena) {
        super(identificador, contrasena);
    }

    public void darDeAltaDoctor(String identificador, String nombre, String especialidad) {
        Doctor doctor = new Doctor(identificador, nombre, especialidad);
        guardarDoctor(doctor);
    }

    public void darDeAltaPaciente(String identificador, String nombre) {
        Paciente paciente = new Paciente(identificador, nombre);
        guardarPaciente(paciente);
    }

    public void agendarCita(String identificador, String fecha, String hora, String motivo, Doctor doctor, Paciente paciente) {
        // Lógica para agendar una cita
        Cita cita = new Cita(identificador, fecha, hora, motivo, doctor, paciente);
        // Guardar los datos en un archivo CSV o en otro formato deseado
        guardarCita(cita);
    }

    private void guardarDoctor(Doctor doctor) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("doctores.csv", true))) {
            writer.write(doctor.getIdentificador() + "," + doctor.getNombre() + "," + doctor.getEspecialidad());
            writer.newLine();
        } catch (IOException e) {
            System.out.println("Error al guardar los datos del doctor: " + e.getMessage());
        }
    }

    private void guardarPaciente(Paciente paciente) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("pacientes.csv", true))) {
            writer.write(paciente.getIdentificador() + "," + paciente.getNombre());
            writer.newLine();
        } catch (IOException e) {
            System.out.println("Error al guardar los datos del paciente: " + e.getMessage());
        }
    }

    private void guardarCita(Cita cita) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter("citas.csv", true))) {
            writer.write(cita.getIdentificador() + "," + cita.getFecha() + "," + cita.getHora() + "," + cita.getMotivo() + "," +
                    cita.getDoctor().getIdentificador() + "," + cita.getPaciente().getIdentificador());
            writer.newLine();
        } catch (IOException e) {
            System.out.println("Error al guardar los datos de la cita: " + e.getMessage());
        }
    }
}

