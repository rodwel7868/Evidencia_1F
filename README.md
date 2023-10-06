# Evidencia_1F
Evidencia 

package citasmedicas;

class Paciente {
    private int id;
    private String nomb;

    public Paciente(int id, String nom) {
        this.id = id;
        this.nomb = nom;
    }

    public int getId() {
        return id;
    }

    public String getNombre() {
        return nomb;
    }

    @Override
    public String toString() {
        return "Paciente [id=" + id + ", nombre=" + nomb + "]";
    }
}
