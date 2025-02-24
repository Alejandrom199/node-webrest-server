import http from "http"
import fs from "fs"

const PORT = 8081

const server = http.createServer((req, res) => {
    //!Ejemplo 1
    // console.log(req.url)

    // res.writeHead(200, { "Content-Type": "text/html" })
    // res.write("<h1>Hola mundo</h1>")
    
    // res.end()

    //!Ejemplo 2
    // const data = {
    //     name: "Juan",
    //     age: 25
    // }

    // res.writeHead(200, { "Content-Type": "application/json" })
    // res.write(JSON.stringify(data)) //Transforma a JSON
    // res.end()

    //!Ejemplo 3
    if((req.url === "/") ) {
        const htmlFile = fs.readFileSync("./public/index.html", "utf-8")
        res.writeHead(200, { "Content-Type": "text/html" })
        res.end(htmlFile)
        return
    }

    if(req.url?.endsWith('.js')){
        res.writeHead(200, {"Content-Type" : "application/javascript"})
    }
    else if(req.url?.endsWith('.css')){
        res.writeHead(200, {"Content-Type" : "text/css"})
    }

    // if(fs.existsSync("./public${req.url}")){
        const responseContent = fs.readFileSync(`.public${req.url}`, "utf-8")
        res.end(responseContent)
    // }
    
})


server.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`)
})