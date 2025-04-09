#include <iostream>
#include <thread>
#include <mutex>
#include <vector>
#include <chrono>
#include <cstdlib>
#include <random>

class Entity {
protected:
    std::string name;
    int health;
    int attack;
    int defense;
public:
    Entity(const std::string& n, int h, int a, int d) 
        : name(n), health(h), attack(a), defense(d) {}
    
    virtual ~Entity() {}
    virtual void displayInfo() const = 0;
    
    bool isAlive() const { return health > 0; }
    void takeDamage(int damage) { health -= damage; }
    int getAttack() const { return attack; }
    int getDefense() const { return defense; }
    std::string getName() const { return name; }
};

class Character : public Entity {
public:
    Character(const std::string& n, int h, int a, int d)
        : Entity(n, h, a, d) {}
    
    void displayInfo() const override {
        std::cout << "Character: " << name << ", HP: " << health 
                  << ", Attack: " << attack << ", Defense: " << defense << std::endl;
    }
};

class Monster : public Entity {
public:
    Monster(const std::string& n, int h, int a, int d)
        : Entity(n, h, a, d) {}
    
    void displayInfo() const override {
        std::cout << "Monster: " << name << ", HP: " << health 
                  << ", Attack: " << attack << ", Defense: " << defense << std::endl;
    }
};

// Глобальные переменные для синхронизации
std::vector<Monster> monsters;
std::mutex monstersMutex;
Character* hero = nullptr;
std::mutex heroMutex;

// Генератор случайных монстров
void generateMonsters() {
    std::random_device rd;
    std::mt19937 gen(rd());
    std::uniform_int_distribution<> healthDist(30, 70);
    std::uniform_int_distribution<> attackDist(5, 20);
    std::uniform_int_distribution<> defenseDist(2, 10);
    
    const std::string monsterNames[] = {"Goblin", "Orc", "Troll", "Skeleton"};
    
    while (true) {
        std::this_thread::sleep_for(std::chrono::seconds(3));
        
        std::uniform_int_distribution<> nameDist(0, 3);
        std::string name = monsterNames[nameDist(gen)];
        int health = healthDist(gen);
        int attack = attackDist(gen);
        int defense = defenseDist(gen);
        
        {
            std::lock_guard<std::mutex> lock(monstersMutex);
            monsters.emplace_back(name, health, attack, defense);
            std::cout << "New monster generated: " << name << std::endl;
        }
    }
}

// Симуляция боя
void battleSimulation() {
    while (true) {
        std::this_thread::sleep_for(std::chrono::seconds(2));
        
        std::lock_guard<std::mutex> heroLock(heroMutex);
        if (!hero || !hero->isAlive()) continue;
        
        std::lock_guard<std::mutex> monsterLock(monstersMutex);
        if (monsters.empty()) continue;
        
        // Выбираем случайного монстра
        std::random_device rd;
        std::mt19937 gen(rd());
        std::uniform_int_distribution<> dist(0, monsters.size() - 1);
        int index = dist(gen);
        Monster& monster = monsters[index];
        
        if (!monster.isAlive()) continue;
        
        // Персонаж атакует монстра
        int heroDamage = hero->getAttack() - monster.getDefense();
        if (heroDamage > 0) {
            monster.takeDamage(heroDamage);
            std::cout << hero->getName() << " hits " << monster.getName() 
                      << " for " << heroDamage << " damage!" << std::endl;
        }
        
        // Монстр атакует персонажа
        if (monster.isAlive()) {
            int monsterDamage = monster.getAttack() - hero->getDefense();
            if (monsterDamage > 0) {
                hero->takeDamage(monsterDamage);
                std::cout << monster.getName() << " hits " << hero->getName() 
                          << " for " << monsterDamage << " damage!" << std::endl;
            }
        }
        
        // Удаляем мертвых монстров
        monsters.erase(
            std::remove_if(monsters.begin(), monsters.end(),
                [](const Monster& m) { return !m.isAlive(); }),
            monsters.end());
        
        // Проверяем состояние персонажа
        if (!hero->isAlive()) {
            std::cout << hero->getName() << " has been defeated!" << std::endl;
            break;
        }
    }
}

int main() {
    // Создаем персонажа
    hero = new Character("Hero", 100, 20, 10);
    
    // Запускаем поток генерации монстров
    std::thread generator(generateMonsters);
    generator.detach();
    
    // Запускаем поток симуляции боя
    std::thread battle(battleSimulation);
    
    // Главный цикл - отображение состояния
    while (true) {
        std::this_thread::sleep_for(std::chrono::seconds(1));
        
        {
            std::lock_guard<std::mutex> heroLock(heroMutex);
            if (hero) {
                hero->displayInfo();
                if (!hero->isAlive()) break;
            }
        }
        
        {
            std::lock_guard<std::mutex> monsterLock(monstersMutex);
            std::cout << "Monsters count: " << monsters.size() << std::endl;
            for (const auto& monster : monsters) {
                monster.displayInfo();
            }
        }
        
        std::cout << "----------------------" << std::endl;
    }
    
    battle.join();
    delete hero;
    return 0;
}
