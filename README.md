# Tienda_de_electronicos.
Código correspondiente al proyecto grupal del curso Introducción a la programación. Universidad Fidelitas.

/*
 * Universidad Fidelitas.
 * Introduccion a la programacion.
 * Hecho por: Grupo 2.
 * Proyecto universitario.
 */
 
package sem6_t.electronicos;


public class Sem6_TElectronicos 
{

    
    public static void main(String[] args) 
    {
        Plataforma tienda = new Plataforma();
        tienda.Menu_principal();
    }
    
}

package sem6_t.electronicos;

import javax.swing.JOptionPane;


public class Plataforma 
{
    Cliente customer= new Cliente();
    Cajas buy= new Cajas();
    Producto pr= new Producto();
    Numero_de_tienda TI= new Numero_de_tienda();
    Oficinas ofi[]=new Oficinas[5];
    Empleado em= new Empleado();
    Bodega bod= new Bodega();
    int Compra= 0,cont=0,cont2=0,con,m=0;
   
    
    public void Menu_principal(){
        int Tienda;
        
        do{
        Tienda= Integer.parseInt(JOptionPane.showInputDialog("Proyeto Tienda de electronicos.\n"
                + "\nIndique la accion que desea llevar a cabo."
                + "\n1.  Iniciar sesion cliente."
                + "\n2.  Cerrar sesion cliente."
                + "\n3.  Compra."
                + "\n4.  Explorar productos."
                + "\n5.  Ver infirmacion cliente."
                + "\n6.  Ver informacion legal."
                + "\n7.  Abrir sesion empleado."
                + "\n8.  Cerrar sesion empleado."
                + "\n9.  Agregar comentario."
                + "\n10. Opciones de bodega."
                + "\n11. Opciones de presupuesto."
                + "\n0. Salir."));
        
        switch(Tienda){
            case 1: Registro();
                break;
            case 2: cerrar_cliente();
                break;
            case 3: 
                if(cont==1 && cont2==1){
                Compras();
                }else{
                    JOptionPane.showMessageDialog(null, "Sesion cliente o empleado no se han iniciado."
                            + "\nAsegurese iniciar ambas sesiones para realizar una compra.");
                }
                break;
            case 4: pr.promociones();
                break;
            case 5: 
                if(cont==0){
                    JOptionPane.showMessageDialog(null, "Aun no hay sesion cliente abierta.");
                }else{
                    customer.informacionCliente();
                }
                break;
            case 6: 
                int opt= Integer.parseInt(JOptionPane.showInputDialog("1. Informacion de todas las tiendas."
                        + "\n2. Buscar con una ubicacion especifica."));
                switch(opt){
                    case 1: TI.buscarTienda(); break;
                    case 2: TI.ubicacion(); break;
                }
                break;
            case 7:
                if(cont2==0){
                em.AbrirSes();
                  cont2++;
                }else{
                    JOptionPane.showMessageDialog(null, "Ya hay una sesion abierta.");
                }
            break;
            case 8:
                if(cont2==1){
                em.CerrarSes();
                  cont2--;
                }else{
                    JOptionPane.showMessageDialog(null, "Ya han cerrado sesion.");
                }
            break;
            case 9: if(m==0){
                        inicializa();
                    }
                    coments();
            break;
            case 10: int op=0;
                do{
                    op= Integer.parseInt(JOptionPane.showInputDialog("OPCIONES DE BODEGA.\n\n¿Que accion desea realizar?"
                            + "\n1. Ver informacion de productos."
                            + "\n2. Adquirir productos."
                            + "\n0. Salir."));
                    switch(op){
                        case 1: bod.cantidades();
                            break;
                        case 2: bod.compra_prod();
                            break;
                        case 0:
                            break;
                        default: JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
                    }
                }while(op!=0);
            break;
            case 11: bod.uso_presupuesto();
                break;
        }
        }while(Tienda!=0);
    }
    
    public void Registro(){
        if(cont<1){
        customer.setNombre(JOptionPane.showInputDialog("Escriba nombre del cliente."));
        customer.setNumero_de_cedula(JOptionPane.showInputDialog("Digite numero de cedula."));
        customer.setNumero_de_telefono(Integer.parseInt(JOptionPane.showInputDialog("Digite numero telefonico.")));
        customer.setCorreo(JOptionPane.showInputDialog("Escriba el correo electronico."));
        
        Compra= Integer.parseInt(JOptionPane.showInputDialog("Los clientes usuales cuentan con un credito inicial"
                + "\nde ₡150.000. Al comprar una membresia su credito"
                + "\ninicial sera de ₡250.000.\n\n"
                + "\n¿Desea adquirir una membresia?"
                + "\n1. Si."
                + "\n2. No"));
        switch(Compra){
            case 1: customer.setMembresia("Activa.");
                    customer.setCredito(250000);
                break;
            case 2: customer.setMembresia("No posee.");
                    customer.setCredito(150000);
                break;
        }
        cont++;
        customer.setTarjeta((int)(Math.random()*99999+10000));

        JOptionPane.showMessageDialog(null, "¡¡Sesion cliente iniciada correctamente!!\n"
                + "\nNombre: "+customer.getNombre()
                + "\nNumero de cedula: "+customer.getNumero_de_cedula()
                + "\nNumero de telefono: "+customer.getNumero_de_telefono()
                + "\nCorreo electronico: "+customer.getCorreo()
                + "\nMembresia: "+customer.getMembresia()
                + "\nSaldo credito: ₡"+customer.getCredito()
                + "\n\nEl numero de tarjeta de membresia temporal es:  "+customer.getTarjeta());
        }else{
            JOptionPane.showMessageDialog(null, "Cupo de clientes lleno.");
        }
    }
    
    public void cerrar_cliente(){
        if(cont>0){
        cont--;
        }else{
            JOptionPane.showMessageDialog(null, "No se ha iniciado ninguna\nsesion cliente.");
        }
    }
    
    public void Compras(){
        int Codigo_del_producto= Integer.parseInt(JOptionPane.showInputDialog("Escriba el codigo del producto que desea comprar."));
        if(Codigo_del_producto<1111 || Codigo_del_producto>1117){
            JOptionPane.showMessageDialog(null, "Producto no encontrado.");
        }
        
        switch(Codigo_del_producto){
            case 1111:  int op= Integer.parseInt(JOptionPane.showInputDialog("Articulo: "+pr.getCategoria1()+""
                    + "\nPrecio: "+pr.getPrecio1()+"\n\n¿Desea comprar este producto?"
                            + "\n1. Si\n2. No"));
                    if(op==1){
                        int ID_cliente= Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia."
                                + "\n\nSi no sabe cual es, digite 0 y seleccione"
                                + "\nla opcion 5 en el menu principal."));
                        
                        if(ID_cliente==customer.getTarjeta()){                     
                            con= Integer.parseInt(JOptionPane.showInputDialog("Cliente:  "+customer.getNombre()+
                                                           "\nCedula:  "+customer.getNumero_de_cedula()
                                                           +"\nCredito actual de:  "+customer.getCredito()
                                                           +"\n\n¿Los datos son correctos?"
                                                                   + "\n1. Continuar."
                                                                   + "\n2. Reintentar."
                                                                   + "\n0. Salir"));
                        }
                            if(con==1){
                                JOptionPane.showMessageDialog(null, "¡¡Compra realizada con exito!!"
                                        + "\n\n**   Factura a nombre de: "+customer.getNombre()+
                                         "\n**   Cedula: "+customer.getNumero_de_cedula()
                                        + "\n**   Correo: "+customer.getCorreo()
                                        + "\n**   Membresia: "+customer.getMembresia()
                                        + "\n\n**   Articulo adquirido: "+pr.getCategoria1()
                                        + "\n**   Codigo del articulo: "+pr.getCodigo_de_barras1()
                                        + "\n**   Pago total de: "+pr.getPrecio1());
                            }                        
                        
                        if(ID_cliente!=customer.getTarjeta() && ID_cliente!=0){
                            JOptionPane.showMessageDialog(null, "cliente no encontrado.");
                        }
                    }
                break;
                     
            case 1112: 
                       op= Integer.parseInt(JOptionPane.showInputDialog("Articulo: "+pr.getCategoria2()+""
                    + "\nPrecio: "+pr.getPrecio2()+"\n\n¿Desea comprar este producto?"
                            + "\n1. Si\n2. No"));
                    if(op==1){
                        int ID_cliente= Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia."
                                + "\n\nSi no sabe cual es, digite 0 y seleccione"
                                + "\nla opcion 5 en el menu principal."));
                        
                        if(ID_cliente==customer.getTarjeta()){                     
                            con= Integer.parseInt(JOptionPane.showInputDialog("Cliente:  "+customer.getNombre()+
                                                           "\nCedula:  "+customer.getNumero_de_cedula()
                                                           +"\nCredito actual de:  "+customer.getCredito()
                                                           +"\n\n¿Los datos son correctos?"
                                                                   + "\n1. Continuar."
                                                                   + "\n2. Reintentar."
                                                                   + "\n0. Salir"));
                        }
                            if(con==1){
                                JOptionPane.showMessageDialog(null, "¡¡Compra realizada con exito!!"
                                        + "\n\n**   Factura a nombre de: "+customer.getNombre()+
                                         "\n**   Cedula: "+customer.getNumero_de_cedula()
                                        + "\n**   Correo: "+customer.getCorreo()
                                        + "\n**   Membresia: "+customer.getMembresia()
                                        + "\n\n**   Articulo adquirido: "+pr.getCategoria2()
                                        + "\n**   Codigo del articulo: "+pr.getCodigo_de_barras2()
                                        + "\n**   Pago total de: "+pr.getPrecio2());
                            }                        
                        
                        if(ID_cliente!=customer.getTarjeta() && ID_cliente!=0){
                            JOptionPane.showMessageDialog(null, "cliente no encontrado.");
                        }
                    }
                break;
                
            case 1113: 
                     op= Integer.parseInt(JOptionPane.showInputDialog("Articulo: "+pr.getCategoria3()+""
                    + "\nPrecio: "+pr.getPrecio3()+"\n\n¿Desea comprar este producto?"
                            + "\n1. Si\n2. No"));
                    if(op==1){
                        int ID_cliente= Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia."
                                + "\n\nSi no sabe cual es, digite 0 y seleccione"
                                + "\nla opcion 5 en el menu principal."));
                        
                        if(ID_cliente==customer.getTarjeta()){                     
                            con= Integer.parseInt(JOptionPane.showInputDialog("Cliente:  "+customer.getNombre()+
                                                           "\nCedula:  "+customer.getNumero_de_cedula()
                                                           +"\nCredito actual de:  "+customer.getCredito()
                                                           +"\n\n¿Los datos son correctos?"
                                                                   + "\n1. Continuar."
                                                                   + "\n2. Reintentar."
                                                                   + "\n0. Salir"));
                        }
                            if(con==1){
                                JOptionPane.showMessageDialog(null, "¡¡Compra realizada con exito!!"
                                        + "\n\n**   Factura a nombre de: "+customer.getNombre()+
                                         "\n**   Cedula: "+customer.getNumero_de_cedula()
                                        + "\n**   Correo: "+customer.getCorreo()
                                        + "\n**   Membresia: "+customer.getMembresia()
                                        + "\n\n**   Articulo adquirido: "+pr.getCategoria3()
                                        + "\n**   Codigo del articulo: "+pr.getCodigo_de_barras3()
                                        + "\n**   Pago total de: "+pr.getPrecio3());
                            }                        
                        
                        if(ID_cliente!=customer.getTarjeta() && ID_cliente!=0){
                            JOptionPane.showMessageDialog(null, "cliente no encontrado.");
                        }
                    }
                break;
                
            case 1114: 
                      op= Integer.parseInt(JOptionPane.showInputDialog("Articulo: "+pr.getCategoria4()+""
                    + "\nPrecio: "+pr.getPrecio4()+"\n\n¿Desea comprar este producto?"
                            + "\n1. Si\n2. No"));
                    if(op==1){
                        int ID_cliente= Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia."
                                + "\n\nSi no sabe cual es, digite 0 y seleccione"
                                + "\nla opcion 5 en el menu principal."));
                        
                        if(ID_cliente==customer.getTarjeta()){                     
                            con= Integer.parseInt(JOptionPane.showInputDialog("Cliente:  "+customer.getNombre()+
                                                           "\nCedula:  "+customer.getNumero_de_cedula()
                                                           +"\nCredito actual de:  "+customer.getCredito()
                                                           +"\n\n¿Los datos son correctos?"
                                                                   + "\n1. Continuar."
                                                                   + "\n2. Reintentar."
                                                                   + "\n0. Salir"));
                        }
                            if(con==1){
                                JOptionPane.showMessageDialog(null, "¡¡Compra realizada con exito!!"
                                        + "\n\n**   Factura a nombre de: "+customer.getNombre()+
                                         "\n**   Cedula: "+customer.getNumero_de_cedula()
                                        + "\n**   Correo: "+customer.getCorreo()
                                        + "\n**   Membresia: "+customer.getMembresia()
                                        + "\n\n**   Articulo adquirido: "+pr.getCategoria4()
                                        + "\n**   Codigo del articulo: "+pr.getCodigo_de_barras4()
                                        + "\n**   Pago total de: "+pr.getPrecio4());
                            }                        
                        
                        if(ID_cliente!=customer.getTarjeta() && ID_cliente!=0){
                            JOptionPane.showMessageDialog(null, "cliente no encontrado.");
                        }
                    }
                break;
                
            case 1115: 
                      op= Integer.parseInt(JOptionPane.showInputDialog("Articulo: "+pr.getCategoria5()+""
                    + "\nPrecio: "+pr.getPrecio5()+"\n\n¿Desea comprar este producto?"
                            + "\n1. Si\n2. No"));
                    if(op==1){
                        int ID_cliente= Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia."
                                + "\n\nSi no sabe cual es, digite 0 y seleccione"
                                + "\nla opcion 5 en el menu principal."));
                        
                        if(ID_cliente==customer.getTarjeta()){                     
                            con= Integer.parseInt(JOptionPane.showInputDialog("Cliente:  "+customer.getNombre()+
                                                           "\nCedula:  "+customer.getNumero_de_cedula()
                                                           +"\nCredito actual de:  "+customer.getCredito()
                                                           +"\n\n¿Los datos son correctos?"
                                                                   + "\n1. Continuar."
                                                                   + "\n2. Reintentar."
                                                                   + "\n0. Salir"));
                        }
                            if(con==1){
                                JOptionPane.showMessageDialog(null, "¡¡Compra realizada con exito!!"
                                        + "\n\n**   Factura a nombre de: "+customer.getNombre()+
                                         "\n**   Cedula: "+customer.getNumero_de_cedula()
                                        + "\n**   Correo: "+customer.getCorreo()
                                        + "\n**   Membresia: "+customer.getMembresia()
                                        + "\n\n**   Articulo adquirido: "+pr.getCategoria5()
                                        + "\n**   Codigo del articulo: "+pr.getCodigo_de_barras5()
                                        + "\n**   Pago total de: "+pr.getPrecio5());
                            }                        
                        
                        if(ID_cliente!=customer.getTarjeta() && ID_cliente!=0){
                            JOptionPane.showMessageDialog(null, "cliente no encontrado.");
                        }
                    }
                break;
                
            case 1116: 
                      op= Integer.parseInt(JOptionPane.showInputDialog("Articulo: "+pr.getCategoria6()+""
                    + "\nPrecio: "+pr.getPrecio6()+"\n\n¿Desea comprar este producto?"
                            + "\n1. Si\n2. No"));
                    if(op==1){
                        int ID_cliente= Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia."
                                + "\n\nSi no sabe cual es, digite 0 y seleccione"
                                + "\nla opcion 5 en el menu principal."));
                        
                        if(ID_cliente==customer.getTarjeta()){                     
                            con= Integer.parseInt(JOptionPane.showInputDialog("Cliente:  "+customer.getNombre()+
                                                           "\nCedula:  "+customer.getNumero_de_cedula()
                                                           +"\nCredito actual de:  "+customer.getCredito()
                                                           +"\n\n¿Los datos son correctos?"
                                                                   + "\n1. Continuar."
                                                                   + "\n2. Reintentar."
                                                                   + "\n0. Salir"));
                        }
                            if(con==1){
                                JOptionPane.showMessageDialog(null, "¡¡Compra realizada con exito!!"
                                        + "\n\n**   Factura a nombre de: "+customer.getNombre()+
                                         "\n**   Cedula: "+customer.getNumero_de_cedula()
                                        + "\n**   Correo: "+customer.getCorreo()
                                        + "\n**   Membresia: "+customer.getMembresia()
                                        + "\n\n**   Articulo adquirido: "+pr.getCategoria6()
                                        + "\n**   Codigo del articulo: "+pr.getCodigo_de_barras6()
                                        + "\n**   Pago total de: "+pr.getPrecio6());
                            }                        
                        
                        if(ID_cliente!=customer.getTarjeta() && ID_cliente!=0){
                            JOptionPane.showMessageDialog(null, "cliente no encontrado.");
                        }
                    }
                break;
                
        }
    }
    
    public void coments(){
        int op2=0;
        do{
            op2= Integer.parseInt(JOptionPane.showInputDialog("Comentarios.\n\n"
                    + "1. Agregar comentarios."
                    + "\n2. Ver comentarios."
                    + "\n0. Salir"));
            switch(op2){
                case 1: reseñas();
                    break;
                case 2: ver_coments();
                    break;
                case 0:
                    break;
                default: JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
            }
        }while(op2!=0);
    }
    
    public void reseñas(){
        if(m<5){
            String Ubic=JOptionPane.showInputDialog("Escriba la ubicacion de la tienda.");
            Ubic.toLowerCase();
        
            if(Ubic.equals("belen")||Ubic.equals("san jose")||Ubic.equals("escazu")||Ubic.equals("guapiles"))
            {
                String Nombre=JOptionPane.showInputDialog("Escriba el nombre del cliente.");
                String Comentarios=JOptionPane.showInputDialog("En esta seccion escriba\nlos comentarios que desea\nagregar.");
        
                ofi[m]= new Oficinas(Ubic, Comentarios, Nombre);
                m++;
                }else{
                JOptionPane.showMessageDialog(null, "Esta ubicacion no esta disponible.\n\nReintente.");
            }
        }else{
            JOptionPane.showMessageDialog(null, "Se ha alcanzado el limite de comentarios.");
            
        }
        
    }
    
    public void ver_coments(){
        int op4=0;
        op4= Integer.parseInt(JOptionPane.showInputDialog("Seleccione los comentarios que\ndesea revisar.\n\n"
                + "1. "+ofi[0].getNombre()
                + "\n2. "+ofi[1].getNombre()
                + "\n3. "+ofi[2].getNombre()
                + "\n4. "+ofi[3].getNombre()
                + "\n5. "+ofi[4].getNombre()
                + "\n\n0. Salir."));
        switch(op4){
            case 1: JOptionPane.showMessageDialog(null, "Ubicacion: "+ofi[0].getUbic()
                                                        + ".\n\nNombre: "+ofi[0].getNombre()
                                                        + ".\n\nComentario: "+ofi[0].getComentarios());
                break;
            case 2: JOptionPane.showMessageDialog(null, "Ubicacion: "+ofi[1].getUbic()
                                                        + ".\n\nNombre: "+ofi[1].getNombre()
                                                        + ".\n\nComentario: "+ofi[1].getComentarios());
                break;
            case 3: JOptionPane.showMessageDialog(null, "Ubicacion: "+ofi[2].getUbic()
                                                        + ".\n\nNombre: "+ofi[2].getNombre()
                                                        + ".\n\nComentario: "+ofi[2].getComentarios());
                break;
            case 4: JOptionPane.showMessageDialog(null, "Ubicacion: "+ofi[3].getUbic()
                                                        + ".\n\nNombre: "+ofi[3].getNombre()
                                                        + ".\n\nComentario: "+ofi[3].getComentarios());
                break;
            case 5: JOptionPane.showMessageDialog(null, "Ubicacion: "+ofi[4].getUbic()
                                                        + ".\n\nNombre: "+ofi[4].getNombre()
                                                        + ".\n\nComentario: "+ofi[4].getComentarios());
                break;
            case 0:
                break;
            default: JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
        }
    }

    public void inicializa(){
        String Ubic="";
        String Comentarios="";
        String Nombre="";
        
        for(int i=0; i<5; i++){
            ofi[i]= new Oficinas(Ubic, Comentarios, Nombre);
        }
    }
}

package sem6_t.electronicos;

import javax.swing.JOptionPane;

public class Producto 
{
     private String Categoria1; private int Codigo_de_barras1; private int Precio1;
     private String Categoria2; private int Codigo_de_barras2; private int Precio2;
     private String Categoria3; private int Codigo_de_barras3; private int Precio3;
     private String Categoria4; private int Codigo_de_barras4; private int Precio4;
     private String Categoria5; private int Codigo_de_barras5; private int Precio5;
     private String Categoria6; private int Codigo_de_barras6; private int Precio6;
     
     Bodega bod= new Bodega();
     
     public Producto(){
         Categoria1= "Refrigerador Telstar.";     Codigo_de_barras1= 1111;
         Categoria2= "Microondas Telstar.";       Codigo_de_barras2= 1112;
         Categoria3= "Olla arrocera Oasis.";   Codigo_de_barras3= 1113;
         Categoria4= "Coffee Maker Oasis.";           Codigo_de_barras4= 1114;
         Categoria5= "Cocina electrica Black and Decker.";               Codigo_de_barras5= 1115;
         Categoria6= "Plantilla electrica Black & Decker.";    Codigo_de_barras6= 1116;
         
         Precio1= 165000;
         Precio2= 25000;
         Precio3= 19000;
         Precio4= 15000;
         Precio5= 16000;
         Precio6= 35000;
     }

    public String getCategoria1() {
        return Categoria1;
    }

    public void setCategoria1(String Categoria1) {
        this.Categoria1 = Categoria1;
    }

    public int getCodigo_de_barras1() {
        return Codigo_de_barras1;
    }

    public void setCodigo_de_barras1(int Codigo_de_barras1) {
        this.Codigo_de_barras1 = Codigo_de_barras1;
    }

    public int getPrecio1() {
        return Precio1;
    }

    public void setPrecio1(int Precio1) {
        this.Precio1 = Precio1;
    }

    public String getCategoria2() {
        return Categoria2;
    }

    public void setCategoria2(String Categoria2) {
        this.Categoria2 = Categoria2;
    }

    public int getCodigo_de_barras2() {
        return Codigo_de_barras2;
    }

    public void setCodigo_de_barras2(int Codigo_de_barras2) {
        this.Codigo_de_barras2 = Codigo_de_barras2;
    }

    public int getPrecio2() {
        return Precio2;
    }

    public void setPrecio2(int Precio2) {
        this.Precio2 = Precio2;
    }

    public String getCategoria3() {
        return Categoria3;
    }

    public void setCategoria3(String Categoria3) {
        this.Categoria3 = Categoria3;
    }

    public int getCodigo_de_barras3() {
        return Codigo_de_barras3;
    }

    public void setCodigo_de_barras3(int Codigo_de_barras3) {
        this.Codigo_de_barras3 = Codigo_de_barras3;
    }

    public int getPrecio3() {
        return Precio3;
    }

    public void setPrecio3(int Precio3) {
        this.Precio3 = Precio3;
    }

    public String getCategoria4() {
        return Categoria4;
    }

    public void setCategoria4(String Categoria4) {
        this.Categoria4 = Categoria4;
    }

    public int getCodigo_de_barras4() {
        return Codigo_de_barras4;
    }

    public void setCodigo_de_barras4(int Codigo_de_barras4) {
        this.Codigo_de_barras4 = Codigo_de_barras4;
    }

    public int getPrecio4() {
        return Precio4;
    }

    public void setPrecio4(int Precio4) {
        this.Precio4 = Precio4;
    }

    public String getCategoria5() {
        return Categoria5;
    }

    public void setCategoria5(String Categoria5) {
        this.Categoria5 = Categoria5;
    }

    public int getCodigo_de_barras5() {
        return Codigo_de_barras5;
    }

    public void setCodigo_de_barras5(int Codigo_de_barras5) {
        this.Codigo_de_barras5 = Codigo_de_barras5;
    }

    public int getPrecio5() {
        return Precio5;
    }

    public void setPrecio5(int Precio5) {
        this.Precio5 = Precio5;
    }

    public String getCategoria6() {
        return Categoria6;
    }

    public void setCategoria6(String Categoria6) {
        this.Categoria6 = Categoria6;
    }

    public int getCodigo_de_barras6() {
        return Codigo_de_barras6;
    }

    public void setCodigo_de_barras6(int Codigo_de_barras6) {
        this.Codigo_de_barras6 = Codigo_de_barras6;
    }

    public int getPrecio6() {
        return Precio6;
    }

    public void setPrecio6(int Precio6) {
        this.Precio6 = Precio6;
    }

     
     public void promociones(){
    JOptionPane.showMessageDialog(null, "***********   Productos a la venta en todas las tiendas   ***********\n\n\n"
            + Categoria1+".                                 Codigo "+Codigo_de_barras1+".  Precio: ₡"+Precio1+"\n"
            + Categoria2+".                                  Codigo "+Codigo_de_barras2+".  Precio: ₡"+Precio2+"\n"
            + Categoria3+".                                  Codigo "+Codigo_de_barras3+".  Precio: ₡"+Precio3+"\n"
            + Categoria4+".                                 Codigo "+Codigo_de_barras4+".  Precio: ₡"+Precio4+"\n"
            + Categoria5+".     Codigo "+Codigo_de_barras5+".  Precio: ₡"+Precio5+"\n"
            + Categoria6+".       Codigo "+Codigo_de_barras6+".  Precio: ₡"+Precio6);
    }
}

package sem6_t.electronicos;

import javax.swing.JOptionPane;


public class Numero_de_tienda 
{
    private String Localizacion1;  private String Horario1;
    private String Localizacion2;  private String Horario2;
    private String Localizacion3;  private String Horario3;
    private String Localizacion4;  private String Horario4;
    private String ID_de_tienda1;
    private String ID_de_tienda2;  
    private String ID_de_tienda3;
    private String ID_de_tienda4;
    
    
    public Numero_de_tienda(){
        Localizacion1= "Belen";     Horario1= "7:00am - 8:00pm";
        Localizacion2= "San Jose";  Horario2= "6:00am - 7:00pm";
        Localizacion3= "Guapiles";  Horario3= "8:00am - 9:00pm";
        Localizacion4= "Escazu";    Horario4= "8:00am - 9:00pm";
        ID_de_tienda1= "TI0107";
        ID_de_tienda2= "TI0101";    
        ID_de_tienda3= "TI0103";
        ID_de_tienda4= "TI0104";
    }
    
    
    public void buscarTienda(){
        //Este metodo permite ingresar a una tienda filtrando todas sus localizaciones.
        JOptionPane.showMessageDialog(null, "Todas las tiendas habilitadas son:\n"
                + "\nTienda "+ID_de_tienda1+".  Ubicacion: "+Localizacion1+".          Horario: "+Horario1+"."
                + "\nTienda "+ID_de_tienda2+".  Ubicacion: "+Localizacion2+".   Horario: "+Horario2+"."
                + "\nTienda "+ID_de_tienda3+".  Ubicacion: "+Localizacion3+".     Horario: "+Horario3+"."
                + "\nTienda "+ID_de_tienda4+".  Ubicacion: "+Localizacion4+".       Horario: "+Horario4+".");
    }
   
    public void ubicacion(){
        //este metodo se encarga de mostrar datos de una tienda en una ubicacion especifica.
        String location= JOptionPane.showInputDialog("Escriba la zona que desea consultar.");
        
        if(location.equals("belen") || location.equals("Belen")){
            JOptionPane.showMessageDialog(null, "Tienda "+ID_de_tienda1+".  Ubicacion: "+Localizacion1+".  Horario: "+Horario1+".");
        }
        if(location.equals("san jose")){
            JOptionPane.showMessageDialog(null, "Tienda "+ID_de_tienda2+".  Ubicacion: "+Localizacion2+".  Horario: "+Horario2+".");
        }
        if(location.equals("guapiles")){
            JOptionPane.showMessageDialog(null, "Tienda "+ID_de_tienda3+".  Ubicacion: "+Localizacion3+".  Horario: "+Horario3+".");
        }
        if(location.equals("escazu")){
            JOptionPane.showMessageDialog(null, "Tienda "+ID_de_tienda4+".  Ubicacion: "+Localizacion4+".  Horario: "+Horario4+".");
        }
        if(!location.equals("belen") && !location.equals("Belen") && !location.equals("san jose") && !location.equals("guapiles") && !location.equals("escazu")){
            JOptionPane.showMessageDialog(null, "No se encuentra ninguna tienda"
                    + "\nen esta ubicacion.");
        }
    }

    public String getLocalizacion1() {
        return Localizacion1;
    }

    public void setLocalizacion1(String Localizacion1) {
        this.Localizacion1 = Localizacion1;
    }

    public String getHorario1() {
        return Horario1;
    }

    public void setHorario1(String Horario1) {
        this.Horario1 = Horario1;
    }

    public String getLocalizacion2() {
        return Localizacion2;
    }

    public void setLocalizacion2(String Localizacion2) {
        this.Localizacion2 = Localizacion2;
    }

    public String getHorario2() {
        return Horario2;
    }

    public void setHorario2(String Horario2) {
        this.Horario2 = Horario2;
    }

    public String getLocalizacion3() {
        return Localizacion3;
    }

    public void setLocalizacion3(String Localizacion3) {
        this.Localizacion3 = Localizacion3;
    }

    public String getHorario3() {
        return Horario3;
    }

    public void setHorario3(String Horario3) {
        this.Horario3 = Horario3;
    }

    public String getLocalizacion4() {
        return Localizacion4;
    }

    public void setLocalizacion4(String Localizacion4) {
        this.Localizacion4 = Localizacion4;
    }

    public String getHorario4() {
        return Horario4;
    }

    public void setHorario4(String Horario4) {
        this.Horario4 = Horario4;
    }

    public String getID_de_tienda1() {
        return ID_de_tienda1;
    }

    public void setID_de_tienda1(String ID_de_tienda1) {
        this.ID_de_tienda1 = ID_de_tienda1;
    }

    public String getID_de_tienda2() {
        return ID_de_tienda2;
    }

    public void setID_de_tienda2(String ID_de_tienda2) {
        this.ID_de_tienda2 = ID_de_tienda2;
    }

    public String getID_de_tienda3() {
        return ID_de_tienda3;
    }

    public void setID_de_tienda3(String ID_de_tienda3) {
        this.ID_de_tienda3 = ID_de_tienda3;
    }

    public String getID_de_tienda4() {
        return ID_de_tienda4;
    }

    public void setID_de_tienda4(String ID_de_tienda4) {
        this.ID_de_tienda4 = ID_de_tienda4;
    }
}

package sem6_t.electronicos;

import javax.swing.JOptionPane;

public class Empleado {

    private String Nombre;
    private String ID;
    private int Num_Gafete;
    private int Celular;
    private String Correo;
    private int cont = 0;

    public Empleado() {
        Nombre = "";
        ID = "";
        Num_Gafete = 0;
        Celular = 0;
        Correo = "";
    }

    public String getNombre() {
        return Nombre;
    }

    public void setNombre(String Nombre) {
        this.Nombre = Nombre;
    }

    public String getID() {
        return ID;
    }

    public void setID(String ID) {
        this.ID = ID;
    }

    public int getNum_Gafete() {
        return Num_Gafete;
    }

    public void setNum_Gafete(int Num_Gafete) {
        this.Num_Gafete = Num_Gafete;
    }

    public int getCelular() {
        return Celular;
    }

    public void setCelular(int Celular) {
        this.Celular = Celular;
    }

    public String getCorreo() {
        return Correo;
    }

    public void setCorreo(String Correo) {
        this.Correo = Correo;
    }

    public void AbrirSes() {
        if (cont == 0) {
            Nombre = (JOptionPane.showInputDialog("Escriba su nombre."));
            ID = (JOptionPane.showInputDialog("Digite su numero de cedula."));
            Celular = (Integer.parseInt(JOptionPane.showInputDialog("Digite su numero telefonico.")));
            Correo = (JOptionPane.showInputDialog("Escriba su correo electronico."));

            JOptionPane.showMessageDialog(null, "¡¡Registro activo!!\n"
                    + "\nNombre: " + Nombre
                    + "\nNumero de cedula: " + ID
                    + "\nNumero de telefono: " + Celular
                    + "\nCorreo electronico: " + Correo
                    + "\n\nAhora puede interactuar con la plataforma."
                            + "\nDigite opcion 8 para cerrar la sesion.");
            cont++;
        } else {
            JOptionPane.showMessageDialog(null, "No se puede registrar porque hay un empleado activo");
        }
    }

    public void CerrarSes() {
        if(cont==1){
        JOptionPane.showMessageDialog(null, "Empleado: "+Nombre +"\nSesion Cerrada");    
        Nombre = "";
        ID = "";
        Num_Gafete = 0;
        Celular = 0;
        Correo = "";
        cont--;
    }else{
            JOptionPane.showMessageDialog(null, "No se ha iniciado ninguna sesion.");
        }
    }

}

package sem6_t.electronicos;

import javax.swing.JOptionPane;

public class Cliente 
{
    private String Numero_de_cedula;
    private String Nombre;
    private String Membresia;
    private int Credito;
    private String Correo;
    private int Numero_de_telefono;
    private int Tarjeta;
    
    public Cliente(){
        Numero_de_cedula= "";
        Nombre= "";
        Membresia= "";
        Credito= 0;
        Correo= "";
        Numero_de_telefono= 0;
        Tarjeta= 0;
    }
    

    public String getNumero_de_cedula() {
        return Numero_de_cedula;
    }

    public void setNumero_de_cedula(String Numero_de_cedula) {
        this.Numero_de_cedula = Numero_de_cedula;
    }

    public String getNombre() {
        return Nombre;
    }

    public void setNombre(String Nombre) {
        this.Nombre = Nombre;
    }

    public String getMembresia() {
        return Membresia;
    }

    public void setMembresia(String Membresia) {
        this.Membresia = Membresia;
    }

    public int getCredito() {
        return Credito;
    }

    public void setCredito(int Credito) {
        this.Credito = Credito;
    }

    public String getCorreo() {
        return Correo;
    }

    public void setCorreo(String Correo) {
        this.Correo = Correo;
    }

    public int getNumero_de_telefono() {
        return Numero_de_telefono;
    }

    public void setNumero_de_telefono(int Numero_de_telefono) {
        this.Numero_de_telefono = Numero_de_telefono;
    }
    
    public int getTarjeta() {
        return Tarjeta;
    }

    public void setTarjeta(int Tarjeta) {
        this.Tarjeta = Tarjeta;
    }
    
    
     public void informacionCliente(){
        JOptionPane.showMessageDialog(null, 
                "****************Informacion cliente***************\n\n\n"
                        + "Cliente 1.\n"
                        + "\nNombre: "+Nombre+
                        "\nNumero de cedula: "+Numero_de_cedula+
                        "\nNumero de telefono: "+Numero_de_telefono+
                        "\nMembresia: "+Membresia+
                        "\nCorreo: "+Correo+
                        "\nNumero tarjeta de membresia: "+Tarjeta+
                        "\nCredito es de: ₡"+Credito);
                        
    }
}

package sem6_t.electronicos;

import javax.swing.JOptionPane;


public class Bodega 
{
    private String[] productos1;
    private String[] productos2;
    private String[] productos3;
    private int[] precio1;
    private int[] precio2;
    private int[] precio3;
    private int[] cant1;
    private int[] cant2;
    private int[] cant3;
    private String[] proveedor;
    int ant=0;
    
    public Bodega(){
        productos1= new String[2];
        productos2= new String[2];
        productos3= new String[2];
        precio1= new int[2];
        precio2= new int[2];
        precio3= new int[2];
        cant1= new int[2];
        cant2= new int[2];
        cant3= new int[2];
        proveedor= new String[3];
        
        productos1[0]="Refrigerador Telstar.";  precio1[0]=165000;              proveedor[0]="Telstar.";
        productos1[1]="Microondas Telstar.";    precio1[1]=25000;  
        productos2[0]="Olla arrocera Oasis.";   precio2[0]=19000;               proveedor[1]="Oasis.";
        productos2[1]="Coffee Maker Oasis.";    precio2[1]=15000;
        productos3[0]="Cocina electrica Black and Decker.";  precio3[0]=16000;  proveedor[2]="Black and Decker.";
        productos3[1]="Plantilla electrica Black & Decker.";  precio3[1]=35000;
        
        cant1[0]=100;
        cant1[1]=100;
        cant2[0]=100;
        cant2[1]=100;
        cant3[0]=100;
        cant3[1]=100;
    }

    Cajas caj= new Cajas();
    
    public String[] getProductos1() {
        return productos1;
    }

    public void setProductos1(String[] productos1) {
        this.productos1 = productos1;
    }

    public String[] getProductos2() {
        return productos2;
    }

    public void setProductos2(String[] productos2) {
        this.productos2 = productos2;
    }

    public String[] getProductos3() {
        return productos3;
    }

    public void setProductos3(String[] productos3) {
        this.productos3 = productos3;
    }

    public int[] getPrecio1() {
        return precio1;
    }

    public void setPrecio1(int[] precio1) {
        this.precio1 = precio1;
    }

    public int[] getPrecio2() {
        return precio2;
    }

    public void setPrecio2(int[] precio2) {
        this.precio2 = precio2;
    }

    public int[] getPrecio3() {
        return precio3;
    }

    public void setPrecio3(int[] precio3) {
        this.precio3 = precio3;
    }

    public String[] getProveedor() {
        return proveedor;
    }

    public void setProveedor(String[] proveedor) {
        this.proveedor = proveedor;
    }
    
    public void cantidades(){
        int selec=0;
        
        do{
        selec= Integer.parseInt(JOptionPane.showInputDialog("Seleccione un proveedor.\n\n"
                + "1. "+proveedor[0]
                + "\n2. "+proveedor[1]
                + "\n3. "+proveedor[2]+"\n\n0. Salir."));
        
        switch(selec){
            case 1: JOptionPane.showMessageDialog(null, "Proveedor: "+proveedor[0]
                                                          +"\nArticulo: "+productos1[0]+"\nPrecio: "+precio1[0]+"\nCantidad: "+cant1[0]
                                                          +"\n\nArticulo: "+productos1[1]+"\nPrecio: "+precio1[1]+"\nCantidad: "+cant1[1]);
                break;
            case 2: JOptionPane.showMessageDialog(null, "Proveedor: "+proveedor[1]
                                                          +"\nArticulo: "+productos2[0]+"\nPrecio: "+precio2[0]+"\nCantidad: "+cant2[0]
                                                          +"\n\nArticulo: "+productos2[1]+"\nPrecio: "+precio2[1]+"\nCantidad: "+cant2[1]);
                break;
            case 3: JOptionPane.showMessageDialog(null, "Proveedor: "+proveedor[2]
                                                          +"\nArticulo: "+productos3[0]+"\nPrecio: "+precio3[0]+"\nCantidad: "+cant3[0]
                                                          +"\n\nArticulo: "+productos3[1]+"\nPrecio: "+precio3[1]+"\nCantidad: "+cant3[1]);
                break;
            case 0:
                break;
            default: JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
        }
    }while(selec!=0);
}
    
    public void compra_prod(){
        int selec=0,selec2=0;
        
        do{
        selec= Integer.parseInt(JOptionPane.showInputDialog("Seleccione un proveedor.\n\n"
                + "1. "+proveedor[0]
                + "\n2. "+proveedor[1]
                + "\n3. "+proveedor[2]+"\n\n0. Salir."));
        
        switch(selec){
            case 1: selec2= Integer.parseInt(JOptionPane.showInputDialog("Seleccione un articulo."
                    + "\n\n1. "+productos1[0]+"\n2. "+productos1[1]));
                 switch(selec2){
                     case 1: int newca= Integer.parseInt(JOptionPane.showInputDialog("Producto: "+productos1[0]
                                        +"\nCantidad de articulos: "+cant1[0]
                                        +"\n\n¿Cuantas unidades se van a adquirir?"));
                     int aux= newca*precio1[0];
                     
                     if(aux<=caj.getPresupuesto()){
                             ant=cant1[0];
                             cant1[0]+=newca;
                             JOptionPane.showMessageDialog(null, "Productos adquiridos.\n\n"
                                                               + productos1[0]+"\nCantidad anterior: "+ant
                                                               +"\nCantidad actual: "+cant1[0]);
                     }else{
                         JOptionPane.showMessageDialog(null, "Presupuesto insuficiente.\nRevise la cantidad.");
                     }
                         break;
                         //
                         //
                         //
                     case 2: newca= Integer.parseInt(JOptionPane.showInputDialog("Producto: "+productos1[1]
                                        +"\nCantidad de articulos: "+cant1[1]
                                        +"\n\n¿Cuantas unidades se van a adquirir?"));
                     aux= newca*precio1[1];
                     
                     if(aux<=caj.getPresupuesto()){
                             ant=cant1[1];
                             cant1[1]+=newca;
                             JOptionPane.showMessageDialog(null, "Productos adquiridos.\n\n"
                                                               + productos1[1]+"\nCantidad anterior: "+ant
                                                               +"\nCantidad actual: "+cant1[1]);
                     }else{
                         JOptionPane.showMessageDialog(null, "Presupuesto insuficiente.\nRevise la cantidad.");
                     }
                         break;
                     default: JOptionPane.showMessageDialog(null, "Debe seleccionar una opcion valida.\nReintente.");
                 }
                break;
                
                
            case 2:selec2= Integer.parseInt(JOptionPane.showInputDialog("Seleccione un articulo."
                    + "\n\n1. "+productos2[0]+"\n2. "+productos2[1]));
                 switch(selec2){
                     case 1: int newca= Integer.parseInt(JOptionPane.showInputDialog("Producto: "+productos2[0]
                                        +"\nCantidad de articulos: "+cant2[0]
                                        +"\n\n¿Cuantas unidades se van a adquirir?"));
                     int aux= newca*precio2[0];
                     
                     if(aux<=caj.getPresupuesto()){
                             ant=cant2[0];
                             cant2[0]+=newca;
                             JOptionPane.showMessageDialog(null, "Productos adquiridos.\n\n"
                                                               + productos2[0]+"\nCantidad anterior: "+ant
                                                               +"\nCantidad actual: "+cant2[0]);
                     }else{
                         JOptionPane.showMessageDialog(null, "Presupuesto insuficiente.\nRevise la cantidad.");
                     }
                         break;
                         //
                         //
                         //
                     case 2: newca= Integer.parseInt(JOptionPane.showInputDialog("Producto: "+productos2[1]
                                        +"\nCantidad de articulos: "+cant2[1]
                                        +"\n\n¿Cuantas unidades se van a adquirir?"));
                     
                              aux= newca*precio2[1];
                     
                     if(aux<=caj.getPresupuesto()){
                             ant=cant2[1];
                             cant2[1]+=newca;
                             JOptionPane.showMessageDialog(null, "Productos adquiridos.\n\n"
                                                               + productos2[1]+"\nCantidad anterior: "+ant
                                                               +"\nCantidad actual: "+cant2[1]);
                     }else{
                         JOptionPane.showMessageDialog(null, "Presupuesto insuficiente.\nRevise la cantidad.");
                     }
                         break;
                     default: JOptionPane.showMessageDialog(null, "Debe seleccionar una opcion valida.\nReintente.");
                 }
                break;
                
                
            case 3:selec2= Integer.parseInt(JOptionPane.showInputDialog("Seleccione un articulo."
                    + "\n\n1. "+productos3[0]+"\n2. "+productos3[1]));
                 switch(selec2){
                     case 1: int newca= Integer.parseInt(JOptionPane.showInputDialog("Producto: "+productos3[0]
                                        +"\nCantidad de articulos: "+cant3[0]
                                        +"\n\n¿Cuantas unidades se van a adquirir?"));
                     
                             int aux= newca*precio3[0];
                     
                     if(aux<=caj.getPresupuesto()){
                             ant=cant3[0];
                             cant3[0]+=newca;
                             JOptionPane.showMessageDialog(null, "Productos adquiridos.\n\n"
                                                               + productos3[0]+"\nCantidad anterior: "+ant
                                                               +"\nCantidad actual: "+cant3[0]);
                     }else{
                         JOptionPane.showMessageDialog(null, "Presupuesto insuficiente.\nRevise la cantidad.");
                     }
                         break;
                         //
                         //
                         //
                     case 2: newca= Integer.parseInt(JOptionPane.showInputDialog("Producto: "+productos3[1]
                                        +"\nCantidad de articulos: "+cant3[1]
                                        +"\n\n¿Cuantas unidades se van a adquirir?"));
                     
                             aux= newca*precio3[1];
                     
                     if(aux<=caj.getPresupuesto()){
                             ant=cant3[1];
                             cant3[1]+=newca;
                             JOptionPane.showMessageDialog(null, "Productos adquiridos.\n\n"
                                                               + productos3[1]+"\nCantidad anterior: "+ant
                                                               +"\nCantidad actual: "+cant3[1]);
                     }else{
                         JOptionPane.showMessageDialog(null, "Presupuesto insuficiente.\nRevise la cantidad.");
                     }
                         break;
                     default: JOptionPane.showMessageDialog(null, "Debe seleccionar una opcion valida.\nReintente.");
                 }
                break;
                
                
            case 0:
                break;
            default: JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
        }
    }while(selec!=0);
    }
    
    public void uso_presupuesto(){
        int op=0;
        
        do{
            op= Integer.parseInt(JOptionPane.showInputDialog("¿Que accion desea realizar?\n\n"
                    + "1. Ver presupuesto."
                    + "\n2. Agregar fondos al presupuesto."
                    + "\n0. Salir"));
            
            switch(op){
                case 1:
                    JOptionPane.showMessageDialog(null, "El presupuesto actual es de:  ₡"+caj.getPresupuesto());
                    break;
                case 2:
                    int nuevo=0;
                    nuevo= Integer.parseInt(JOptionPane.showInputDialog("Digite la cantidad que desea\nagregar al presupuesto."));
                    nuevo+=caj.getPresupuesto();
                    caj.setPresupuesto(nuevo);
                    JOptionPane.showMessageDialog(null, "********** Agregado con exito. **********\n\n"
                            + "El presupuesto ahora es de: ₡"+caj.getPresupuesto());
                    break;
                case 0:
                    break;
                default: JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
            }
        }while(op!=0);
    }
}

package sem6_t.electronicos;


public class Cajas 
{   
    private int presupuesto;
    
    public Cajas(){
        presupuesto= 1000000;
    }
    
    
    public int getPresupuesto() {
        return presupuesto;
    }

    public void setPresupuesto(int presupuesto) {
        this.presupuesto = presupuesto;
    }
    
}

package sem6_t.electronicos;


public class Oficinas 
{
    private String Ubic;
    private String Comentarios;
    private String Nombre;
    
    public Oficinas(String Ubic, String Comentarios, String Nombre){
        this.Ubic=Ubic;
        this.Comentarios=Comentarios;
        this.Nombre=Nombre;
    }

    public String getUbic() {
        return Ubic;
    }

    public void setUbic(String Ubic) {
        this.Ubic = Ubic;
    }

    public String getComentarios() {
        return Comentarios;
    }

    public void setComentarios(String Comentarios) {
        this.Comentarios = Comentarios;
    }
    public String getNombre() {
        return Nombre;
    }

    public void setNombre(String Nombre) {
        this.Nombre = Nombre;
    }
    
}

