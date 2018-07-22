# express-typescript<br/>

<p><blockquote cite="http://krishna-kv.blogspot.com/2017/05/express-js-using-typescript-and-visual.html"> Express is a light-weight web application framework to help organize your web application into an MVC architecture on the server side. TypeScript enables us to develop a solid web applications using Express on Node.js.</blockquote></p>
<ol>
  <li>npm start </li>
   <p style="margin-left:35px">It is used to run the project in development, it will reload the project while the source get changed. </p>
  <li>npm run build:prod</li>
  <p style="margin-left:35px"> It is used for the production build, which uses the webpack-cli for the build and provides a single output file with required additional file such as package.json, configuration files. <br/>
   The output file name and the files to copy can be managed in webpack.config.js 
  </p>
</ol>
<b>To run the project</b>
http://localhost:40401/
  
<p>
  Database Connectivity: <br/>
  Sequelize is used to connect the database. The configuration is managed in config.{env}.json. The dialect options is used to configured the database server.  
  
  <pre class="brush:js;toolbar:false;"><span style="color: #33cccc;">"DBConnections": {
      "default": {
        "user": "sa",
        "password": "sql@123",
        "options": {
          "host": "localhost", // server name
          "database": "testdb", // database name
          "requestTimeout": 300000,
          "dialect": "mssql",
          "operatorsAliases": false,
          "logging": true, //Enable the sequelize logger for queries for dev mode.
          "dialectOptions": {
            "encrypt": false
          }
        }
      }
    }</span></pre>
</p>

  <b>How to pass the Parameter to SQL Query</b> <br/>
  <p style="margin-left:20px">If the JSON and parameter name are same, we can pass the json object to the sql manager as below: <br/>
        public addCustomer(customer: ICustomer) {
        let query = "INSERT INTO customers (name,address) VALUES(:Name,:Address)";
        return this.db.Insert(query, customer);
    }
  </p>
   <b>Adding parameter without JSON Object</b><br/>
 <p style="margin-left:20px"> 
  public deleteCustomer(id) {
        let query = "DELETE FROM customers WHERE Id=:id";
        this.db.addInputParameter("id", id);
        return this.db.Delete(query);
    }
 </p>  
 
 <p>http://localhost:40401/customers</b>
 
 <b>Integrated Swagger UI.</b> 
 Add the swagger json in swagger-docs. Ref customer.swagger.json 
 
 Swagger.controller.ts for adding the swagger routes.
export class SwaggerController {

    public static configure(app: Express) {
        app.use('/swagger/customer', swaggerUi.serve, swaggerUi.setup(customer)); //route for the swagger ui
    }
}

To run the swagger example 
http://localhost:40401/swagger/customer


https://www.initpals.com/node-js/express-js-application-seed-project-with-typescript/<br/>
https://www.initpals.com/node-js/how-to-use-json-based-configuration-in-express-js/
