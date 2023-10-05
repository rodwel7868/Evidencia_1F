# Evidencia_1F
Evidencia 2 

package citasmedicas;

class Cita {
    private String identificador;
    private String fecha;
    private String hora;
    private String motivo;
    private Doctor doctor;
    private Paciente paciente;

    public Cita(String identificador, String fecha, String hora, String motivo, Doctor doctor, Paciente paciente) {
        this.identificador = identificador;
        this.fecha = fecha;
        this.hora = hora;
        this.motivo = motivo;
        this.doctor = doctor;
        this.paciente = paciente;
    }

    public String getIdentificador() {
        return identificador;
    }

    public String getFecha() {
        return fecha;
    }

    public String getHora() {
        return hora;
    }

    public String getMotivo() {
        return motivo;
    }

    public Doctor getDoctor() {
        return doctor;
    }

    public Paciente getPaciente() {
        return paciente;
    }
}
