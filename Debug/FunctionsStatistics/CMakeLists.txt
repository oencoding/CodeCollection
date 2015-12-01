########################################################################################
##########            ���� functions_statisticslib ���ļ�                    ########### 
########################################################################################
LIST (APPEND functions_statistics_LIB_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/FunctionsStatistics.cpp
    )


########################################################################################
#############               ���� functions_statisticslib ��汾��                    ############## 
########################################################################################
set(functions_statistics_LIB_VERSION     "1.0.0")
set(functions_statistics_LIB_SOVERSION   "1")



########################################################################################
##########            ���� ������ļ������ͷ�ļ�Ŀ¼                        ########### 
########################################################################################
include_directories(  
    ${PROJECT_SOURCE_DIR}/includes  
    ${PROJECT_SOURCE_DIR}/Log   
    ${PROJECT_SOURCE_DIR}/Log/FunctionsStatistics
)  
  
  
########################################################################################
##########            ���� ���ӿ��ļ�Ŀ¼                                    ########### 
########################################################################################
link_directories(  
    /usr/local/lib   
    )  

    
########################################################################################
##########        ����Ŀ����ļ� ��������Ҫ������ ����������ϵ               ########### 
########################################################################################
IF (COMPONENT_functions_statistics)
    #���ɶ�̬��  ��̬���� STATIC  
    add_library (functions_statisticslib SHARED         ${functions_statistics_LIB_SRCS})  
    add_library (functions_statistics STATIC            ${functions_statistics_LIB_SRCS})  
    
    # ����������ϵ�������ǰ������ײ�Ĺ����⣬����Ҫ����
    add_dependencies (functions_statisticslib   pthread)
    add_dependencies (functions_statistics      pthread)
    
    # ����Ҫ���ӵĹ�����, ���˳����Ǳ�����������ʱ˳��
    target_link_libraries (functions_statisticslib  pthread)
    target_link_libraries (functions_statistics     pthread)
    
    # ���ð汾�ţ�SOVERSIONΪAPI�汾��
    set_target_properties(functions_statisticslib   PROPERTIES 
                            VERSION     ${functions_statistics_LIB_VERSION} 
                            SOVERSION   ${functions_statistics_LIB_SOVERSION} )

ELSE (COMPONENT_functions_statistics)
    MESSAGE(STATUS "Not Include functions_statistics module.")
ENDIF (COMPONENT_functions_statistics)



########################################################################################
#############                 ����Ŀ�������ļ�                          ############## 
########################################################################################
IF (TEST_MODULE_FLAG)
    add_executable(Testfunctions_statistics.elf    functions_statisticsTest.cpp)
    add_dependencies(Testfunctions_statistics.elf          functions_statisticslib )
    target_link_libraries(Testfunctions_statistics.elf     functions_statisticslib )

ELSE (TEST_MODULE_FLAG)
    MESSAGE(STATUS "Not Include jsoncpp module.")
ENDIF (TEST_MODULE_FLAG)


