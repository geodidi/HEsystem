# HEsystem
A data marketplace system for computation over sensitive data.

# Client Installation
In order to set up the library and interact with encrypted data, you need to follow these steps:
1. Download the repository as a *.zip file*
1. Decompress the *.zip file* and copy the *hesystem* folder to your working directory
1. Import the client library in your python script with: ```import hesystem.client as cl```
1. Search for the data details URL of the organization where you want to buy data
1. Interact with the data following their instructions and our documentation

# Server Installation
In order to set up the library and serve encrypted data from your organization, you need to follow these steps:
1. Download the repository as a *.zip file*
1. Create a *.txt file* and save it as ```/info/user_info.txt``` with your user information. It should look like:
```
address:0x514AEa42dA89B7856C81bdAA4A20BD7D64EbA8E4
private_key:5D232502101181CADEF51F19294A981E22D2DCA38AB031E9BA6EE12F512263BA
endpoint_url:https://ropsten.infura.io/v3/52c1338c6a2220d4a18dfef32ba53c2a
```
1. Create a *.txt file* and save it as ```/info/contract_info.txt``` with the data to sell information. It should look like:
```
meta_link:http://127.0.0.1:5000/data
test_link:http://127.0.0.1:5000/test
test_result_link:http://127.0.0.1:5000/receivedtest
data_link:http://127.0.0.1:5000/restaurants
result_link:http://127.0.0.1:5000/receivedtensor
num_rows:(12,5)
value:20
expiration_time:10
condition:2
```
1. Test the web application by following the steps in the **For Developers** section of this tutorial
1. Upload the web application to a hosting service (remember to change the links in the *contract_info.txt* according to your new server


# Client Documentation
This Homomorphic encryption library allows to compute primitive operations over encrypted data (addition, multiplication and comparisons). With these operations available we can build more complex algorithms in order to extract useful information from encrypted data. The data object inherits some properties from heavily-used machine learning and data analysis libraries. Specifically, it has some properties from the torch.Tensor object ([torch library](https://pytorch.org/)) and also some properties from the np.ndarray object ([Numpy library](https://numpy.org/)). The following documentation describes the most used functions that can be applied to the data object from the HEsystem library. The examples assumes that the variable ```data``` contains the encrypted data sended from the server system of this same library.

1. **data + 3**: outputs the matrix array added 3 to all its internal elements
1. **data - 3**: outputs the matrix array substracted 3 to all its internal elements
1. **data * 3**: outputs the matrix array multiplied by 3 to all its internal elements
1. **data / 3**: outputs the matrix array divided by 3 to all its internal elements
1. **data + encrypted_matrix**: outputs the sum of the two elements
1. **data + decrypted_matrix**: outputs the sum of the two elements
1. **data * encrypted_matrix**: outputs an error because it would take years to compute a multiplication between encrypted numbers
1. **data * decrypted_matrix**: outputs the sum of the two elements
1. **data > matrix**: outputs a matrix of 1s (True) and 0s (False) depending on the condition between the elements
1. **data < matrix**: outputs a matrix of 1s (True) and 0s (False) depending on the condition between the elements
1. **data >= matrix**: outputs a matrix of 1s (True) and 0s (False) depending on the condition between the elements
1. **data <= matrix**: outputs a matrix of 1s (True) and 0s (False) depending on the condition between the elements
1. **data[i]**: outputs the i-th element of the data array. 
1. **data[i][j]**: outputs the ij-ith element of the data matrix.
1. **data.dim()**: outputs the dimensions of the data as a set (for example, if the data is a 5x3 matrix then the output would be (2))
1. **data.t()**: outputs the transpose matrix of the data matrix
1. **data.transpose()**: outputs the transpose matrix of the data matrix
1. **data.mean()**: outputs the mean of all the elements of the data matrix
1. **data.max()**: outputs the largest element of the data matrix
1. **data.min()**: outputs the smallest element of the data matrix
1. **data.mean(1)**: outputs the means of all the rows of the data matrix
1. **data.max(1)**: outputs the largest elements of all the rows of the data matrix
1. **data.min(1)**: outputs the smallest elements of all the rows of the data matrix


# For Developers
## Creatting a Virtual Environment
In order to avoid confusion with existing installed libraries and to keep the dependencies as specific as possible we use virtual environments. To create a Python virtual environment run the following command in the working directory:
```python -m venv environment_name```
To activate the environment run the following command in the working directory:
```
cd environment_name/Scripts/
./ activate
```
## Setting up Flask
To use the flask web server Python's library we need to set the following environment variables:
### Windows
1. ```set FLASK_APP="app.py"```
1. ```set FLASK_ENV="development"``` *(use the development feature only when using an existing contract. For contract deployment, use the production environment)*
1. ```set DATABASE_URL="postgresql://postgres:postgres@localhost:5432/basic-provider"```

### Linux
1. ```$env:FLASK_APP="app.py"```
1. ```$env:FLASK_ENV="development"``` *(use the development feature only when using an existing contract. For contract deployment, use the production environment)*
1. ```$env:DATABASE_URL="postgresql://postgres:postgres@localhost:5432/basic-provider"```

In case you need here is a ["Deploying a Flask Application to Heroku"](https://stackabuse.com/deploying-a-flask-application-to-heroku/) tutorial.
In case you need help about how to point the git repository to the Heroku repository check this [website](https://dashboard.heroku.com/apps/basic-provider/deploy/heroku-git)
In case you need to save dependencies in a *requirements.txt* file (required by Heroku) run the following command:
``` pip freeze > requirements.txt ```
1. If you installed *web3* remember to delete pywin23 dependencies (2 for now) from the requirements.txt files
1. If you are deploying in a free tier Heroku remember to reconfigure torch to use CPU-only by adding this at the top of the torch dependency: ``` --find-links https://download.pytorch.org/whl/torch_stable.html ```

# Acknowledges
We would like to thank the support and collaboration of PhD. Fredy Cuenca and the [PySyft Team](https://github.com/OpenMined/PySyft). 

# Disclaimer
This library is in its development and research phase. Do not use it in a production environment yet.
