using Microsoft.EntityFrameworkCore;

public class BibliotecaDbContext : DbContext
{
    public BibliotecaDbContext(DbContextOptions<BibliotecaDbContext> options) : base(options) { }

    public DbSet<Usuario> Usuarios { get; set; }
    public DbSet<Libro> Libros { get; set; }
    public DbSet<Autor> Autores { get; set; }
    public DbSet<Categoria> Categorias { get; set; }
    public DbSet<Editorial> Editoriales { get; set; }
    public DbSet<Prestamo> Prestamos { get; set; }
    public DbSet<DetallePrestamo> DetallesPrestamo { get; set; }
    public DbSet<RolUsuario> RolesUsuarios { get; set; }
    public DbSet<Reserva> Reservas { get; set; }
    public DbSet<Multa> Multas { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);

        // Relaciones muchos a muchos personalizadas, si las necesitas más detalladas
        modelBuilder.Entity<DetallePrestamo>()
            .HasOne(dp => dp.Prestamo)
            .WithMany(p => p.Detalles)
            .HasForeignKey(dp => dp.PrestamoId);

        modelBuilder.Entity<DetallePrestamo>()
            .HasOne(dp => dp.Libro)
            .WithMany(l => l.DetallesPrestamo)
            .HasForeignKey(dp => dp.LibroId);
    }
}

