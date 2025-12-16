// Create Event of obj_dialogue_manager
dialogue_index = 0;
dialogues = [
    "Welcome to our story...", 
    "This moment feels emotional...",
    "Suddenly, danger approaches!",
    "But then, a funny thing happens..."
];
dialogue_state = 0; // 0 = normal, 1 = thriller, 2 = comedy

// Step Event of obj_dialogue_manager
if (keyboard_check_pressed(vk_space)) {
    dialogue_index += 1;
    if (dialogue_index >= array_length(dialogues)) {
        dialogue_index = 0; // loop or end scene
    }
}

// Draw Event of obj_dialogue_manager
draw_set_color(c_white);
draw_set_font(fnt_dialogue);
draw_text(50, room_height - 100, dialogues[dialogue_index]);

// Create Event of obj_dialogue_manager
dialogue_index = 0;
mood = 50; // 0 = sad/thriller, 100 = happy/comedy
dialogues = [
    ["Welcome to our story...", 50],
    ["This moment feels emotional...", 30],
    ["Suddenly, danger approaches!", 10],
    ["But then, a funny thing happens...", 80]
];

// Step Event of obj_dialogue_manager
if (keyboard_check_pressed(vk_space)) {
    dialogue_index += 1;
    if (dialogue_index >= array_length(dialogues)) {
        dialogue_index = 0;
    }
    
    // Adjust mood based on current dialogue
    mood = dialogues[dialogue_index][1];
}

// Draw Event of obj_dialogue_manager
draw_set_font(fnt_dialogue);
var text = dialogues[dialogue_index][0];

// Change text color based on mood
if (mood < 30) {
    draw_set_color(c_red); // thriller/emotional
} else if (mood > 70) {
    draw_set_color(c_lime); // comedy/happy
} else {
    draw_set_color(c_white); // neutral
}

draw_text(50, room_height - 100, text);

// Optional: Screen tint effect based on mood
if (mood < 30) {
    draw_set_color(make_color_rgba(50, 0, 0, 100));
    draw_rectangle(0, 0, room_width, room_height, false);
} else if (mood > 70) {
    draw_set_color(make_color_rgba(0, 50, 0, 100));
    draw_rectangle(0, 0, room_width, room_height, false);
}

// Create Event of obj_fight_manager
fight_state = "idle"; // idle, attack, defend
player_health = 100;
enemy_health = 100;

// Step Event of obj_fight_manager
if (fight_state == "idle") {
    if (keyboard_check_pressed(ord('A'))) {
        fight_state = "attack";
    } else if (keyboard_check_pressed(ord('D'))) {
        fight_state = "defend";
    }
} else if (fight_state == "attack") {
    enemy_health -= 10;
    fight_state = "idle";
} else if (fight_state == "defend") {
    player_health += 5; // small heal
    fight_state = "idle";
}

// Draw Event of obj_fight_manager
var health_text = "Player HP: " + string(player_health) + " | Enemy HP: " + string(enemy_health);
draw_set_color(c_white);
draw_text(50, 50, health_text);
draw_text(50, 80, "Press 'A' to Attack, 'D' to Defend");

if (player_health <= 0) {
    draw_text(room_width/2 - 50, room_height/2, "You Lose!");
}
if (enemy_health <= 0) {
    draw_text(room_width/2 - 50, room_height/2, "You Win!");
}

fight_state = "idle"; // idle, attack, defend
player_health = 100;
enemy_health = 100;

if (fight_state == "idle") {
    if (keyboard_check_pressed(ord('A'))) {
        fight_state = "attack";
    } else if (keyboard_check_pressed(ord('D'))) {
        fight_state = "defend";
    }
} else if (fight_state == "attack") {
    enemy_health -= 10;
    fight_state = "idle";
} else if (fight_state == "defend") {
    player_health += 5; // small heal
    fight_state = "idle";
}

var health_text = "Player HP: " + string(player_health) + " | Enemy HP: " + string(enemy_health);
draw_set_color(c_white);
draw_text(50, 50, health_text);
draw_text(50, 80, "Press 'A' to Attack, 'D' to Defend");

if (player_health <= 0) {
    draw_text(room_width/2 - 50, room_height/2, "You Lose!");
}
if (enemy_health <= 0) {
    draw_text(room_width/2 - 50, room_height/2, "You Win!");
}
