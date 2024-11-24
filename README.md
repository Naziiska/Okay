import React, { useState } from 'react';
import { View, Text, TextInput, Button, FlatList } from 'react-native';

const App = () => {
  const [task, setTask] = useState('');
  const [tasks, setTasks] = useState([]);

  const addTask = () => {
    setTasks([...tasks, { id: tasks.length.toString(), name: task }]);
    setTask('');
  };

  const deleteTask = (id) => {
    setTasks(tasks.filter((task) => task.id !== id));
  };

  return (
    <View style={{ padding: 20 }}>
      <TextInput
        placeholder="Enter task"
        value={task}
        onChangeText={setTask}
        style={{ borderWidth: 1, marginBottom: 10, padding: 10 }}
      />
      <Button title="Add Task" onPress={addTask} />
      <FlatList
        data={tasks}
        renderItem={({ item }) => (
          <View style={{ flexDirection: 'row', justifyContent: 'space-between', padding: 10 }}>
            <Text>{item.name}</Text>
            <Button title="Delete" onPress={() => deleteTask(item.id)} />
          </View>
        )}
        keyExtractor={(item) => item.id}
      />
    </View>
  );
};

export default App;
