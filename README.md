# MACROLOG #
A simple head-only log system. 

You must include two directories, ```include``` and ```iter/include```. 

## Requirements ##
Compile option: --std=c++11 

## Log settings ##
The default log destination is ```stderr```.

You can redirect the log destination of each level by using:
```
iter::SetLogDestination(iter::INFO, "notice.log");
iter::SetLogDestination(iter::WARN | iter::ERROR | iter::FATAL, "warning.log");
```

Compile options:
* ```-DDEBUG``` : Enable debug log.
* ```-DITER_LOG_DISABLE``` : Disable all of the logs.

## Example ##
Code 1:
```
double pi = 3.1415926;

ITER_DEBUG_KV("TAG", MSG("KV log test."), KV("pi", pi));
ITER_INFO_KV("TAG", MSG("KV log test."), KV(pi));
ITER_WARN_KV(MSG("KV log test."), KV(pi));
ITER_ERROR_KV(MSG("KV log test."), KV(pi));
ITER_FATAL_KV(MSG("KV log test."), KV(pi));
```
Output 1:
```
[DEBUG][2017-01-19T21:37:50.671+0800][527] TAG||msg=KV log test.||pi=3.1415926
[INFO][2017-01-19T21:37:50.672+0800][527] TAG||msg=KV log test.||pi=3.1415926
[WARN][2017-01-19T21:37:50.672+0800][527] msg=KV log test.||pi=3.1415926
[ERROR][2017-01-19T21:37:50.672+0800][527] msg=KV log test.||pi=3.1415926
[FATAL][2017-01-19T21:37:50.672+0800][527] msg=KV log test.||pi=3.1415926
```
Code 2:
```
std::map <std::string, int> mp = 
    {std::make_pair("map_1", 1), std::make_pair("map_2", 2)};
    
std::vector <std::pair <std::string, double>> vec = 
    {std::make_pair("vec_1", 3.3), std::make_pair("vec_2", 4.4)};
    
std::list <std::tuple <std::string, int>> lst = 
    {std::make_tuple("list_1", 5), std::make_tuple("list_2", 6)};

ITER_INFO_KV(MSG("Map, vector and list test."), mp, vec, lst);
```
Output 2:
```
[INFO][2017-01-19T21:37:50.672+0800][527] msg=Map, vector and list test.||map_1=1||map_2=2||vec_1=3.3||vec_2=4.4||list_1=5||list_2=6
```
