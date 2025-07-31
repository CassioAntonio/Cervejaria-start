# Cervejaria 
\

import React, { useState } from 'react';
import { View, Text, TextInput, Button, StyleSheet, TouchableOpacity, ScrollView } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import Animated, { withTiming, useSharedValue, useAnimatedStyle } from 'react-native-reanimated';

// Tela de Introdução (Landing Page)
function LandingScreen({ navigation }) {
  return (
    <View style={styles.landingContainer}>
      <Text style={styles.landingHeader}>Cerveja Breedom!</Text>
      <Text style={styles.landingDescription}>
       Se for pra brindar, que seja com uma campeã!
      </Text>
      <TouchableOpacity style={styles.landingButton} onPress={() => navigation.navigate('Home')}>
        <Text style={styles.landingButtonText}>Começar</Text>
      </TouchableOpacity>
    </View>
  );
}

// Tela Inicial
function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.header}>Queridinhas Premiada</Text>
      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate('Area')}
      >
        <Text style={styles.buttonText}>Larger</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate('Equation')}
      >
        <Text style={styles.buttonText}>Ipa</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate('Formulas')}
      >
        <Text style={styles.buttonText}>Session Ipa</Text>
      </TouchableOpacity>
    </View>
  );
}

// Tela de Cálculo de Área
function AreaScreen() {
  const [shape, setShape] = useState('');
  const [dimension, setDimension] = useState('');
  const [result, setResult] = useState(null);

  const handleCalculate = () => {
    let area = 0;
    if (shape === 'círculo') {
      area = Math.PI * Math.pow(Number(dimension), 2);
    } else if (shape === 'quadrado') {
      area = Math.pow(Number(dimension), 2);
    } else if (shape === 'triângulo') {
      area = (Math.pow(Number(dimension), 2) * Math.sqrt(3)) / 4;
    }
    setResult(area.toFixed(2));
  };

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Larger</Text>
    </View>
  );
}

// Tela de Resolver Equações
function EquationScreen() {
  const [equation, setEquation] = useState('');
  const [solution, setSolution] = useState(null);

  const handleSolve = () => {
    try {
      const solved = eval(equation); // Resolve a equação simples
      setSolution(solved);
    } catch (error) {
      setSolution('Erro na equação');
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Ipa</Text>
      {solution !== null && <Text style={styles.result}>Resultado: {solution}</Text>}
    </View>
  );
}

// Tela de Fórmulas Matemáticas com animação
function FormulasScreen() {
  const fadeAnim = useSharedValue(0);

  const animatedStyle = useAnimatedStyle(() => {
    return {
      opacity: withTiming(fadeAnim.value, { duration: 1500 }),
    };
  });

  React.useEffect(() => {
    fadeAnim.value = 1; // Iniciar a animação quando a tela for carregada
  }, [fadeAnim]);

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Session Ipa</Text>
      <Animated.View style={[styles.formulaContainer, animatedStyle]}>
        <ScrollView>
          
        </ScrollView>
      </Animated.View>
    </View>
  );
}

// Configuração da navegação
const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Landing">
        <Stack.Screen name="Landing" component={LandingScreen} options={{ headerShown: false }} />
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Area" component={AreaScreen} />
        <Stack.Screen name="Equation" component={EquationScreen} />
        <Stack.Screen name="Formulas" component={FormulasScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

const styles = StyleSheet.create({
  landingContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#6a5acd',
    padding: 20,
  },
  landingHeader: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#ffa500',
    marginBottom: 20,
  },
  landingDescription: {
    fontSize: 18,
    color: 'white',
    textAlign: 'center',
    marginBottom: 30,
  },
  landingButton: {
    backgroundColor: '#FF5722',
    paddingVertical: 12,
    paddingHorizontal: 40,
    borderRadius: 25,
  },
  landingButtonText: {
    fontSize: 20,
    color: 'white',
  },
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#6a5acd',
  },
  topHeader: {
    position: 'absolute', // Faz o texto ficar fixo no topo
    top: 50, // Ajuste a distância do topo conforme necessário
    left: 20, // Para ajustar a distância da margem esquerda
    fontSize: 24,
    fontWeight: 'bold',
    color: 'white',
    zIndex: 1,
  },
  header: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  input: {
    width: '80%',
    padding: 10,
    borderWidth: 1,
    borderColor: '#ddd',
    marginBottom: 20,
    borderRadius: 5,
  },
  button: {
    backgroundColor: '#FF5722',
    paddingVertical: 12,
    paddingHorizontal: 40,
    borderRadius: 25,
    marginBottom: 10,
  },
  buttonText: {
    fontSize: 18,
    color: 'white',
  },
  result: {
    fontSize: 18,
    fontWeight: 'bold',
    marginTop: 20,
    color: 'green',
  },
  formulaContainer: {
    width: '100%',
    padding: 10,
  },
  formula: {
    fontSize: 18,
    marginVertical: 10,
  },
});












