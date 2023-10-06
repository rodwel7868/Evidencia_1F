# Evidencia_1F
Evidencia 

package citasmedicas;

class Doctor {
    private int id;
    private String nom;
    private String espec;

    public Doctor(int id, String nomb, String especial) {
        this.id = id;
        this.nom = nomb;
        this.espec = especial;
    }

    public int getId() {
        return id;
    }

    public String getNombre() {
        return nom;
    }

    public String getEspecialidad() {
        return espec;
    }

    @Override
    public String toString() {
        return "Doctor [id=" + id + ", nombre=" + nom + ", especialidad=" + espec + "]";
    }
}
