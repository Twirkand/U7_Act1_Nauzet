```java
public boolean create(Employee employee) {
        Connection connection = null;
        try {
            connection = getConnection();
            PreparedStatement sentencia = connection
                    .prepareStatement("INSERT INTO employee VALUES (?, ?, ?)");
            sentencia.setInt(1, employee.getId());
            sentencia.setString(2, employee.getName());
            if (employee.getReportsTo() == null) {
                sentencia.setNull(5, java.sql.Types.INTEGER);
            } else {
                sentencia.setInt(5, employee.getReportsTo());
            }
            return sentencia.executeUpdate() > 0;
@Override
    public Employee findById(Integer id) {
        Connection connection = null;
        try {
            connection = getConnection();
            PreparedStatement sentencia = connection.prepareStatement("SELECT * FROM employee WHERE id=?");
            sentencia.setInt(1, id);
            ResultSet resultado = sentencia.executeQuery();
            if (!resultado.next())
                return null;
            String name = resultado.getString("name");
            Integer reportsTo = (Integer) resultado.getObject("reports_to");
            Integer rolId = resultado.getInt("rol_id");
            Employee empleado = new Employee(id, name, reportsTo);
            return empleado;
@Override
    public List<Employee> findAll() {
        Connection connection = null;
        try {
            connection = getConnection();
            PreparedStatement sentencia = connection.prepareStatement("SELECT * FROM employee");
            ResultSet resultado = sentencia.executeQuery();
            List<Employee> empleados = new ArrayList<>();
            while (resultado.next()) {
                int id = resultado.getInt("id");
                String name = resultado.getString("name");
                Integer reportsTo = (Integer) resultado.getObject("reports_to");
                Employee empleado = new Employee(id, name, reportsTo);
                empleados.add(empleado);
            }
            return empleados;
@Override
    public boolean deleteById(Integer id) {
        Connection connection = null;
        try {
            connection = getConnection();
            PreparedStatement sentencia = connection.prepareStatement("DELETE FROM employee WHERE id=?");
            sentencia.setInt(1, id);
            return sentencia.executeUpdate() == 1;
``
