const { Worker } = require('worker_threads');
 
function sumVectors(vectorA, vectorB) {
    return new Promise((resolve, reject) => {
        const worker = new Worker('./child.js', { workerData: { vectorA, vectorB } });
 
        worker.on('message', (result) => resolve(result));
 
        worker.on('error', (error) => reject(error));
        worker.on('exit', (code) => {
            if (code !== 0) {
                reject(new Error(Worker finalizado con código ${code}));
            }
        });
    });
}
 
const vectorA = [1, 2, 3];
const vectorB = [5, 6, 7];
 
sumVectors(vectorA, vectorB)
    .then(result => console.log('Resultado de la suma:', result))
    .catch(err => console.error('Error:', err));# parents.js
