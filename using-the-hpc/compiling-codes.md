# Compiling Codes

## C, Fortran Examples

coming soon.

## MPI Example

```text
 //hello_mpi.c

 #include
 #include

int main(int argc, char** argv) {
  // Initialize the MPI environment
  MPI_Init(NULL, NULL);
  // Get the number of processes
  int world_size;
  MPI_Comm_size(MPI_COMM_WORLD, &world_size);
  // Get the rank of the process
  int world_rank;
  MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);
  // Get the name of the processor
  char processor_name[MPI_MAX_PROCESSOR_NAME];
  int name_len;
  MPI_Get_processor_name(processor_name, &name_len);
  // Print off a hello world message
  printf("Hello world from processor %s, rank %d  out of %d processors\n", processor_name, world_rank, world_size);
  // Finalize the MPI environment.
  MPI_Finalize();
  }
```

To compile mpi example, please load gcc and openmpi modules. After loading the modules, use gcc to compile hello\_mpi.c. For example,

```text
module load gcc/5.3.0
module load openmpi/2.0.0
gcc $OPENMPI_INC -o mpi_test.o -c mpi_test.c
```

## CUDA/GPU Example

coming soon.

## IDL Example

coming soon.

